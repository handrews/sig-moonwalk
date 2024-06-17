
 <style>
/* Override the default respec styling */
pre > code { background: hsl(24, 20%, 95%); display: block; padding: 1em; margin: .5em 0; overflow: auto; border-radius: 0; }
h1,h2,h3 { color: #629b34; }
p#w3c-state { color: #629b34; }
p#dt-published { color: #629b34; }
a[href] { color: #45512c; }
body:not(.toc-inline)
toc h2 { color: #45512c; }
body:not(.toc-inline) #toc h2 { color: #45512c; }
table { display: block; width: 100%; overflow: auto; }
table th { font-weight: 600; }
table th, table td { padding: 6px 13px; border: 1px solid #dfe2e5; }
table tr { background-color: #fff; border-top: 1px solid #c6cbd1; }
table tr:nth-child(2n) { background-color: #f6f8fa; }
pre { background-color: #f6f8fa !important; }
</style> 
<section class="introductory">

# Current Status of Document

This contents of this document have been gathered from a combination of the 3.1 specification and proposed changes for Moonwalk. <strong>None of the content in this document should be considered as product of consensus.</strong>  This is a working document for the purposes of getting the mechanics of publishing a document in place and beginning to discuss the overall structure of the document.
</section>

<section id="abstract">
The OpenAPI Specification (OAS) defines a standard, programming language-agnostic interface description for HTTP APIs, which allows both humans and computers to discover and understand the capabilities of a service without requiring access to source code, additional documentation, or inspection of network traffic. When properly defined via OpenAPI, a consumer can understand and interact with the remote service with a minimal amount of implementation logic. Similar to what interface descriptions have done for lower-level programming, the OpenAPI Specification removes guesswork in calling a service.

</section>

<section id="conformance" class="introductory">

This document is licensed under [The Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.html).

</section>


# Introduction

# Definitions

## IRIs and URLs

term                    | scheme        | fragment  | character set
----------------------- | ------------- | ----------| -------------
IRI                     | required      | allowed   | UTF-8
IRI-reference           | allowed       | allowed   | UTF-8
relative IRI-reference  | forbidden     | allowed   | UTF-8
absolute-IRI            | required      | forbidden | UTF-8
URI                     | required      | allowed   | US-ASCII
URI-reference           | allowed       | allowed   | US-ASCII
relative URI-reference  | forbidden     | allowed   | US-ASCII
absolute-URI            | required      | forbidden | US-ASCII


## OpenAPI Description

A document or set of documents that:

1. Are parsed and linked in accordance with [Parsing and Serializing Description Documents](#parsing-and-serializing-description-documents)
2. Describe an API's shape, deployment, or both, based on the identified entry document

### Entry Document

The document within an OpenAPI Description where parsing begins.

### OpenAPI Shape Description

An OpenAPI description that 
# Specification

## API Description Documents

### The API Description Model

This defines an in-memory representation of the graph resulting from parsing an OpenAPI Description.
This data structure is to be defined in a way that is portable across programming languages and environments.
The structure is a graph to ensure that internal linkages are retained and handled consistently, rather than being elided in an attempt to force descriptions to behave like trees.

It MUST be possible to serialize the graph into any major graph database system (RDF/SPARQL, Apache TinkerPop Gremlin, OpenCypher, GQL, etc.).  This is a requirement to ensure cross-environment interoperability.
It MUST be possible to implement an editor on top of a graph representation.
Editors and similar tools MAY be implemented in terms of a graph database, but this is not required; it is expected that language-native in-memory representations will be common.

### Parsing and Serializing Description Documents

### Resolving Description Document URIs

### Retrieving and Loading Documents


#### Input

## Working with Data

This section specifies how to model data syntax and semantics.
It covers abstract data modeling, as well as parsing and serialization based on media types or grammars, and projecting into domains such as code (SDKs) or interfaces (web forms).

The Schema Object is the central data model, together with a registry specifying how it maps to various media types (e.g. `application/xml`, `application/x-www-form-urlencoded`, or `multipart/form-data`) or grammars (e.g. RFC8491 "Structure Field Values fo HTTP"'s `sf-list / sf-dictionary / sf-item` rules or RFC9110 "HTTP Semantics"'s `field-value` rule).

_NOTE:_ Also need to map to interfaces (SDK functions/methods, web forms)

* 2-way mappings:
    * Media Types
        * HTTP message [content](https://www.rfc-editor.org/rfc/rfc9110.html#name-content)
        * URL (or IRI?) query strings (`application/x-www-form-urlencoded`)
    * Grammars
        * HTTP [fields](https://www.rfc-editor.org/rfc/rfc9110.html#name-fields) (headers and trailers)
* 1-way mappings (may be "2-way-ish" for test generators)
    * Interfaces
        * SDK functions or methods
        * Web forms (including for interactive documentation)

No matter the location, a data model is a data model, represented by a [Schema Object](#schemaObject).



Data needs to be parsed out of and serialized into various representations, each of which uses one or more auxilliary objects for disambiguation:

* The [Encoding Object](#encoding-object) maps models to media types or grammar-based formats
* The [Code Object](#code-object) provides additional information on types and relationships relevant to code generation
* The [Input Object](#input-object) provides additional information on constructing input forms, whether they are intended for UI rendering or programmatic use

Some mappings will be ambiguous given the limitations of the JSON Schema data model; in such cases an [Encoding Object]() is used to 
* Media types or grammars (Encoding Object)
* 

### Correlating Objects

The Schema Object remains the primary data model, however, several Objects are used to fit that model to other domains: input forms, code, media types, and grammar-defined formats.
There are two possible ways to correlate these objects, each of which has is pros and cons.

?? **MAPPING OBJECT?** Generic form or correlating object?

#### Embedding Objects

This approach generalizes 3.x's XML Object and Discriminator Object while also placing strict bounds on what the general form can and cannot do.
It could be structured either as one extension keyword per object, as in 3.x, or as a single `oas` (or similar) keyword with many sub-objects.
Using a single `oas` keyword is appealing as it creates a single point of connection between standard and OAS-extended JSON Schemas, which would only require implementing a single plug-in for each JSON Schema implementation that supports extension vocabularies.
In either approach, the keyword(s) will be _annotations_, and MUST NOT impact the validation outcome.

The Schema Object should do the minimal data definition necessary to enable the other Objects to complete the job.
This might require some shifts in mindset 

* **Pros:** The full expressive power of JSON Schema

### The Schema Object

### Supplemental Objects

There are two possible ways to structure the supplemental objects:

1. Inline, as one or more schema extension keywords; it would be best to use a single `oas` extension keyword, which would be an (possibly templatized like hyperschema?) annotation; we would need to think about interactions with `$ref` and combinatorics
1. Separate and associated via _selectors_

#### The Form Object
-> Does this go with the requests in the HTTP section?  Yes, because it's about usage of data, not about data.

The form object replaces aspects of the Parameter Object that correlate input data structure to the core data model.
However, it is not limited to URI Templates
Defines inputs and maps them to data model elements.
URI Tempate stuff goes here?

#### The Encoding Object

Maps data model elements to media type or grammar elements.
This object does not care about how or in what context the mapping is used.
    * Does that mean there is one per target rather than one per source or one per source+target pair?

Encoding Object:
    * "when this value is binary, encode it as a string using base64"
    * "use a nested multipart here"
    * "route this to element, this to attribute, this to text"
    * same input form could be encoded differently into JSON, form-urlencoded, form-data, etc.

#### The Code Object

Indicates how the data model structure maps into higher-level programming language concepts like inheritance (class-based or prototype-based?  Does anyone still use prototype inheritance in JavaScript?).

## API Shapes

Dependencies: [Working with Data](#working-with-data), 

This section describes the shape of the API by modeling the HTTP operations.
It models HTTP messages in the same way that API data is modeled, and builds on that to describe the relationships among HTTP messages that produce its interaction semantics.
Relationships include correlating responses to requests, grouping operations by resource, and grouping related resources such as collections and items.
Signature definition and matching is also described here.

### The HTTP Data Model (RFC9110 §6)

A data model (specifically one with a well-defined mapping to `application/http` [[RFC9112]]) into which message-specific data models are inserted, and over which interactions are defined.

* ?Framing?
    * Implicit vs length-delimited
* Control data
    * Requests
        * Request Method
        * Request Target
        * Protocol Version
    * Reponses
        * Status Code
        * Reason Phrase [OPTIONAL]
        * Protocol Version
    * Notes: "Via" header field protocol shenanigans
* Headers lookup table
    * Ordered sequence
    * Multi-line vs single-line for multiple values?
* Content stream (potentially unbounded)
    * Does not include encodings such as chunked; model after that is processed
    * 1xx, 204, 304 no content
    * All other reesponses codes have (possibly 0-length) content
* Trailers lookup table
    * Same as headers, structurally

One approach would be an ultra-generic modeling of the HTTP message abstraction (RFC9110 §6):
```YAML
$comment: Generic HTTP message structure
type: object
required:
- control
- headers
properties:
  control:
    type: object
    oneOf:
    - $comment: Request
      required:
      - method
      - target
      properties:
        method:
          type: string
        target:
          type: string
          format: uri # iri for our purposes?
    - $comment: Response
      required:
      - status
      properties:
        status:
          type: string
  headers:
    $ref: "#/$defs/fields"
  content:
    $comment: Data Model goes here!
  trailers:
    $ref: "#/$defs/fields"
$defs:
  fields:
    type: array
    items:
      type: object
      properties:
        name:
          type: string
        value:
          $comment: Data Model goes here!
```
From this generic base, we could pull out specific items that are better handled as special cases (also need to think about what _should not_ be modeled in OAS):

* `Content-Type` is better associated with `content` than `headers`; this might be true for all representation metadata (RFC9110 §8)
* Validator fields (§8.8) are a special area within content metadata
* Authentication (§11) probably better abstracted with other auth things than treated as a generic part of HTTP fields, etc.

Need to think about how HTTP Operation interfaces are used- e.g. `Accept` and similar headers are inputs to a request, but not usually thought of in the same way as query string parameters.  HTML forms map to `form-urlencoded` or `form-data`, but SDKs might map parameters into bits and pieces of a body, for example.  This is important for workflows.

In many cases, we don't so much want to model the fields as we want to model some aspect of their meanings or usage.  You wouldn't model ETags in detail, but you might want to know whether they are expected to be used, and whether to expect weak or strong ones.

### Operation Object

* Groups Requests and Responses

### Input Object

* Maps from an input interface (SDK function/method, web form, etc.) to one or more data models

* Multiple Input Objects per request - "sub-"operations?

## API Deployment

### API Discoverability

### API Security

## API Documentation

## Specification Extensions

# Security Considerations

<section class="appendix">

# Revision History

Version   | Date       | Notes
---       | ---        | ---
3.1.0     | 2021-02-15 | Release of the OpenAPI Specification 3.1.0 
3.1.0-rc1 | 2020-10-08 | rc1 of the 3.1 specification
3.1.0-rc0 | 2020-06-18 | rc0 of the 3.1 specification
3.0.3     | 2020-02-20 | Patch release of the OpenAPI Specification 3.0.3
3.0.2     | 2018-10-08 | Patch release of the OpenAPI Specification 3.0.2
3.0.1     | 2017-12-06 | Patch release of the OpenAPI Specification 3.0.1
3.0.0     | 2017-07-26 | Release of the OpenAPI Specification 3.0.0
3.0.0-rc2 | 2017-06-16 | rc2 of the 3.0 specification
3.0.0-rc1 | 2017-04-27 | rc1 of the 3.0 specification
3.0.0-rc0 | 2017-02-28 | Implementer's Draft of the 3.0 specification
2.0       | 2015-12-31 | Donation of Swagger 2.0 to the OpenAPI Initiative
2.0       | 2014-09-08 | Release of Swagger 2.0
1.2       | 2014-03-14 | Initial release of the formal document.
1.1       | 2012-08-22 | Release of Swagger 1.1
1.0       | 2011-08-10 | First release of the Swagger Specification

</section>

<section class="appendix" id="issue-summary">
  <!-- A list of issues will magically appear here -->
</section>
