
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


### Parsing and Serializing Description Documents

### Resolving Description Document URIs

#### Input

## Working with Data

This section specifies how to model data syntax and semantics.
It covers abstract data modeling, as well as parsing and serialization based on media types or grammars, and projecting into domains such as code (SDKs) or interfaces (web forms).

## API Shapes

Dependencies: [Working with Data](#working-with-data), 

This section describes the shape of the API by modeling the HTTP operations.
It models HTTP messages in the same way that API data is modeled, and builds on that to describe the relationships among HTTP messages that produce its interaction semantics.
Relationships include correlating responses to requests, grouping operations by resource, and grouping related resources such as collections and items.
Signature definition and matching is also described here.

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
