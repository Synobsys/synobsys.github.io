# API Design rules

## Abstract

This document contains a normative standard for designing APIs.

## Introduction

### Goal

More and more organizations offer REST APIs (henceforth abbreviated as APIs), in addition to existing interfaces like SOAP and WFS. These APIs aim to be developer-friendly and easy to implement. While this is a commendable aim, it does not shield a developer from a steep learning curve getting to know every new API, in particular when every individual API is designed using different patterns and conventions.

This document aims to describe a widely applicable set of design rules for the unambiguous provisioning of REST APIs. The primary goal is to offer guidance for organizations designing new APIs, with the purpose of increasing developer experience (DX) and interoperability between APIs.

### Status

Concept

## Summary

<aside class="note">
Design rules have unique and permanent numbers. In the event of design rules being deprecated or restructured, they are removed from the list. Therefore, gaps in the sequence can occur. New design rules will always get a new and higher number.
</aside>

### Normative Design Rules

* <a href="#api-01">API-01</a>: Adhere to HTTP safety and idempotency semantics for operations
* <a href="#api-02">API-02</a>: Do not maintain session state on the server
* <a href="#api-03">API-03</a>: Only apply standard HTTP methods
* <a href="#api-04">API-04</a>: Define interfaces in English
* <a href="#api-05">API-05</a>: Use nouns to name resources
* <a href="#api-06">API-06</a>: Use nested URIs for child resources
* <a href="#api-07">API-07</a>: Model resource operations as a sub-resource or dedicated resource
* <a href="#api-08">API-08</a>: Use OpenAPI Specification for documentation
* <a href="#api-09">API-09</a>: Publish documentation in English
* <a href="#api-10">API-10</a>: Include a deprecation schedule when publishing API changes
* <a href="#api-11">API-11</a>: Schedule a fixed transition period for a new major API version
* <a href="#api-12">API-12</a>: Include the major version number in the URI
* <a href="#api-13">API-13</a>: Leave off trailing slashes from URIs
* <a href="#api-14">API-14</a>: Publish OAS document at a standard location in JSON-format
* <a href="#api-15">API-15</a>: Hide irrelevant implementation details
* <a href="#api-16">API-16</a>: Use plural nouns to name collection resources
* <a href="#api-17">API-17</a>: Publish a changelog for API changes between versions
* <a href="#api-18">API-18</a>: Adhere to the Semantic Versioning model when releasing API changes
* <a href="#api-57">API-19</a>: Return the full version number in a response header

## The Design Rules

### Resources

The REST architectural style is centered around the concept of a [resource](#dfn-resource). A resource is the key abstraction of information, where every piece of information is named by assigning a globally unique [URI](#dfn-uri) (Uniform Resource Identifier). Resources describe *things*, which can vary between physical objects (e.g. a building or a person) and more abstract concepts (e.g. a permit or an event).

<div class="rule" id="api-05">
  <p class="rulelab"><b>API-05</b>: Use nouns to name resources</p>
  <p>Because resources describe things (and thus not actions), resources are referred to using nouns (instead of verbs) that are relevant from the perspective of the user of the API.</p>
  <div class="example">
    <p>A few correct examples of nouns as part of a URI:</p>
    <ul>
      <li>Location</li>
      <li>Customer</li>
    </ul>
    <p>This is different than RPC-style APIs, where verbs are often used to perform certain actions:</p>
    <ul>
      <li>Request</li>
      <li>Register</li>
    </ul>
  </div>
</div>

A resource describing a single thing is called a [singular resource](#dfn-singular-resource). Resources can also be grouped into collections, which are resources in their own right and can typically be paged, sorted and filtered. Most often all collection members have the same type, but this is not necessarily the case. A resource describing multiple things is called a [collection resource](#dfn-collection-resource). Collection resources typically contain references to the underlying singular resources.

<div class="rule" id="api-16">
  <p class="rulelab"><b>API-16</b>: Use plural nouns to name collection resources</p>
  <p>Because a collection resource represents multiple things, the path segment describing the name of the collection resource must be written in the plural form.</p>
  <div class="example">
    <p>Example collection resources, describing a list of things:</p>
    <pre>https://api.example.org/v1/locations<br/>https://api.example.org/v1/permits</pre>
  </div>
  <p>Singular resources contained within a collection resource are generally named by appending a path segment for the identification of each individual resource.</p>
  <div class="example">
    <p>Example singular resource, contained within a collection resource:</p>
    <pre>https://api.example.org/v1/locations/3b9710c4-6614-467a-ab82-36822cf48db1<br/>https://api.example.org/v1/permits/d285e05c-6b01-45c3-92d8-5e19a946b66f</pre>
  </div>
  <p>Singular resources that stand on their own, i.e. which are not contained within a collection resource, must be named with a path segment that is written in the singular form.</p>
  <div class="example">
    <p>Example singular resource describing the profile of the currently authenticated user:</p>
    <pre>https://api.example.org/v1/userprofile</pre>
  </div>
</div>

<div class="rule" id="api-04">
  <p class="rulelab"><b>API-04</b>: Define interfaces in English</p>
  <p>Since we are publishing APIs for an international audience is the reason to define interfaces in English.</p>
  <p>Note that glossaries exist that define useful sets of attributes which should preferably be reused. Examples can be found at <a href="http://schema.org/docs/schemas.html">schema.org</a>.</p>
</div>

<div class="rule" id="api-13">
  <p class="rulelab"><b>API-13</b>: Leave off trailing slashes from URIs</p>
  <p>According to the URI specification [[rfc3986]], URIs may contain a trailing slash. However, for REST APIs this is considered as a bad practice since a URI including or excluding a trailing slash might be interpreted as different resources (which is strictly speaking the correct interpretation).</p>
  <p>To avoid confusion and ambiguity, a URI must never contain a trailing slash. When requesting a resource including a trailing slash, this must result in a 404 (not found) error response and not a redirect. This enforces API consumers to use the correct URI.</p>
  <div class="example">
    <p>URI without a trailing slash (correct):</p>
    <pre>https://api.example.org/v1/locations</pre>
    <p>URI with a trailing slash (incorrect):</p>
    <pre>https://api.example.org/v1/locations/</pre>
  </div>
</div>

<div class="rule" id="api-15">
  <p class="rulelab"><b>API-15</b>: Hide irrelevant implementation details</p>
  <p>An API should not expose implementation details of the underlying application. The primary motivation behind this design rule is that an API design must focus on usability for the client, regardless of the implementation details under the hood. The API, application and infrastructure need to be able to evolve independently to ease the task of maintaining backwards compatibility for APIs during an agile development process.</p>
  <p>A few examples of implementation details:</p>
  <ul>
    <li>The API design should not necessarily be a 1-on-1 mapping of the underlying domain- or persistence model</li>
    <li>The API should not expose information about the technical components being used, such as development platforms/frameworks or database systems</li>
    <li>The API should offer client-friendly attribute names and values, while persisted data may contain abbreviated terms or serializations which might be cumbersome for consumption</li>
  </ul>
</div>

### HTTP methods

Although the REST architectural style does not impose a specific protocol, REST APIs are typically implemented using HTTP [[rfc7231]].

<div class="rule" id="api-03">
  <p class="rulelab"><b>API-03</b>: Only apply standard HTTP methods</p>
  <p>The HTTP specification [[rfc7231]] and the later introduced <code>PATCH</code> method specification [[rfc5789]] offer a set of standard methods, where every method is designed with explicit semantics. Adhering to the HTTP specification is crucial, since HTTP clients and middleware applications rely on standardized characteristics. Therefore, resources must be retrieved or manipulated using standard HTTP methods.</p>
  <table>
    <thead>
      <tr>
        <th scope="col">Method</th>
        <th scope="col">Operation</th>
        <th scope="col">Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>GET</code></td>
        <td>Read</td>
        <td>Retrieve a resource representation for the given URI. Data is only retrieved and never modified.</td>
      </tr>
      <tr>
        <td><code>POST</code></td>
        <td>Create</td>
        <td>Create a subresource as part of a collection resource. This operation is not relevant for singular resources. This method can also be used for <a href="#api-10">exceptional cases</a>.</td>
      </tr>
      <tr>
        <td><code>PUT</code></td>
        <td>Create/update</td>
        <td>Create a resource with the given URI or replace (full update) a resource when the resource already exists.</td>
      </tr>
      <tr>
        <td><code>PATCH</code></td>
        <td>Update</td>
        <td>Partially updates an existing resource. The request only contains the resource modifications instead of the full resource representation.</td>
      </tr>
      <tr>
        <td><code>DELETE</code></td>
        <td>Delete</td>
        <td>Remove a resource with the given URI.</td>
      </tr>
    </tbody>
  </table>
  <p>The following table shows some examples of the use of standard HTTP methods:</p>
  <table>
    <thead>
      <tr>
        <th scope="col">Request</th>
        <th scope="col">Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>GET /companies</code></td>
        <td>Retrieves a list of companies.</td>
      </tr>
      <tr>
        <td><code>GET /companies/12</code></td>
        <td>Retrieves an individual company.</td>
      </tr>
      <tr>
        <td><code>POST /companies</code></td>
        <td>Creates a new company.</td>
      </tr>
      <tr>
        <td><code>PUT /companies/12</code></td>
        <td>Modifies company #12 completely.</td>
      </tr>
      <tr>
        <td><code>PATCH /companies/12</code></td>
        <td>Modifies company #12 partially.</td>
      </tr>
      <tr>
        <td><code>DELETE /companies/12</code></td>
        <td>Deletes company #12.</td>
      </tr>
    </tbody>
  </table>
  <p class="note">HTTP also defines other methods, e.g. <code>HEAD</code>, <code>OPTIONS</code> and <code>TRACE</code>. For the purpose of this design rule, these operations are left out of scope.</p>
</div>

<div class="rule" id="api-01">
  <p class="rulelab"><b>API-01</b>: Adhere to HTTP safety and idempotency semantics for operations</p>
  <p>The HTTP protocol [[rfc7231]] specifies whether an HTTP method should be considered safe and/or idempotent. These characteristics are important for clients and middleware applications, because they should be taken into account when implementing caching and fault tolerance strategies.</p>
  <p>Request methods are considered <i>safe</i> if their defined semantics are essentially read-only; i.e., the client does not request, and does not expect, any state change on the origin server as a result of applying a safe method to a target resource. A request method is considered <i>idempotent</i> if the intended effect on the server of multiple identical requests with that method is the same as the effect for a single such request.</p>
  <p>The following table describes which HTTP methods must behave as safe and/or idempotent:</p>
  <table>
    <thead>
      <tr>
        <th scope="col">Method</th>
        <th scope="col">Safe</th>
        <th scope="col">Idempotent</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>GET</code></td>
        <td>Yes</td>
        <td>Yes</td>
      </tr>
      <tr>
        <td><code>HEAD</code></td>
        <td>Yes</td>
        <td>Yes</td>
      </tr>
      <tr>
        <td><code>OPTIONS</code></td>
        <td>Yes</td>
        <td>Yes</td>
      </tr>
      <tr>
        <td><code>POST</code></td>
        <td>No</td>
        <td>No</td>
      </tr>
      <tr>
        <td><code>PUT</code></td>
        <td>No</td>
        <td>Yes</td>
      </tr>
      <tr>
        <td><code>PATCH</code></td>
        <td>No</td>
        <td>No</td>
      </tr>
      <tr>
        <td><code>DELETE</code></td>
        <td>No</td>
        <td>Yes</td>
      </tr>
    </tbody>
  </table>
</div>

### Statelessness

One of the key constraints of the REST architectural style is stateless communication between client and server. It means that every request from client to server must contain all of the information necessary to understand the request. The server cannot take advantage of any stored session context on the server as it didn???t memorize previous requests. Session state must therefore reside entirely on the client.

To properly understand this constraint, it's important to make a distinction between two different kinds of state:

* *Session state*: information about the interactions of an end user with a particular client application within the same user session, such as the last page being viewed, the login state or form data in a multi-step registration process. Session state must reside entirely on the client (e.g. in the user's browser).
* *Resource state*: information that is permanently stored on the server beyond the scope of a single user session, such as the user's profile, a product purchase or information about a building. Resource state is persisted on the server and must be exchanged between client and server (in both directions) using  representations as part of the request or response payload. This is actually where the term *REpresentational State Transfer (REST)* originates from.

<p class="note">It's a misconception that there should be no state at all. The stateless communication constraint should be seen from the server's point of view and states that the server should not be aware of any <em>session state</em>.</p>

Stateless communication offers many advantages, including:

* *Simplicity* is increased because the server doesn't have to memorize or retrieve session state while processing requests
* *Scalability* is improved because not having to incorporate session state across multiple requests enables higher concurrency and performance
* *Observability* is improved since every request can be monitored or analyzed in isolation without having to incorporate session context from other requests
* *Reliability* is improved because it eases the task of recovering from partial failures since the server doesn't have to maintain, update or communicate session state. One failing request does not influence other requests (depending on the nature of the failure of course).

<div class="rule" id="api-02">
  <p class="rulelab"><b>API-02</b>: Do not maintain session state on the server</p>
  <p>In the context of REST APIs, the server must not maintain or require any notion of the functionality of the client application and the corresponding end user interactions. To achieve full decoupling between client and server, and to benefit from the advantages mentioned above, no session state must reside on the server. Session state must therefore reside entirely on the client.</p>
  <p class="note">The client of a REST API could be a variety of applications such as a browser application, a mobile or desktop application and even another server serving as a backend component for another client. REST APIs should therefore be completely client-agnostic.</p>
</div>

### Relationships

Resources are often interconnected by relationships. Relationships can be modelled in different ways depending on the cardinality, semantics and more importantly, the use cases and access patterns the REST API needs to support.

<div class="rule" id="api-06">
  <p class="rulelab"><b>API-06</b>: Use nested URIs for child resources</p>
  <p>When having a child resource which can only exist in the context of a parent resource, the URI should be nested. In that case, the child resource does not necessarily have a top-level collection resource. The best way to explain this design rule is by example.</p>
  <div class="example">
    <p>When modelling resources for a news platform including the ability for users to write comments, it might be a good strategy to model the <a href="#dfn-collection-resource">collection resources</a> hierarchically:</p>
    <pre>https://api.example.org/v1/articles/123/comments</pre>
    <p>The platform might also offer a photo section, where the same commenting functionality is offered. In the same way as for articles, the corresponding sub-collection resource might be published at:</p>
    <pre>https://api.example.org/v1/photos/456/comments</pre>
    <p>These nested sub-collection resources can be used to post a new comment (<code>POST</code> method) and to retrieve a list of comments (<code>GET</code> method) belonging to the parent resource, i.e. the article or photo. An important consideration is that these comments could never have existed without the existence of the parent resource.</p>
    <p>From the consumer's perspective, this approach makes logical sense, because the most obvious use case is to show comments below the parent article or photo (e.g. on the same web page) including the possibility to paginate through the comments. The process of posting a comment is separate from the process of publishing a new article. Another client use case might also be to show a global <em>latest comments</em> section in the sidebar. For this use case, an additional resource could be provided:</p>
    <pre>https://api.example.org/v1/comments</pre>
    <p>If this would have not been a meaningful use case, this resource should not exist at all. Because it doesn't make sense to post a new comment from a global context, this resource would be read-only (only <code>GET</code> method is supported) and may possibly provide a more compact representation than the parent-specific sub-collections.</p>
    <p>The <a href="#dfn-singular-resource">singular resources</a> for comments, referenced from all 3 collections, could still be modelled on a higher level to avoid deep nesting of URIs (which might increase complexity or problems due to the URI length):</p>
    <pre>https://api.example.org/v1/comments/123<br />https://api.example.org/v1/comments/456</pre>
    <p>Although this approach might seem counterintuitive from a technical perspective (we simply could have modelled a single <code>/comments</code> resource with optional filters for article and photo) and might introduce partially redundant functionality, it makes perfect sense from the perspective of the consumer, which increases developer experience.</p>
  </div>
</div>

### Operations

<div class="rule" id="api-07">
  <p class="rulelab"><b>API-07</b>: Model resource operations as a sub-resource or dedicated resource</p>
  <p>There are resource operations which might not seem to fit well in the CRUD interaction model. For example, approving of a submission or notifying a customer. Depending on the type of the operation, there are three possible approaches:</p>
  <ol>
    <li>Re-model the resource to incorporate extra fields supporting the particular operation. For example, an approval operation can be modelled in a boolean attribute <code>approved</code> that can be modified by issuing a <code>PATCH</code> request against the resource. Drawback of this approach is that the resource does not contain any metadata about the operation (when and by whom was the approval given? Was the submission declined in an earlier stage?). Furthermore, this requires a fine-grained authorization model, since approval might require a specific role.</li>
    <li>Treat the operation as a sub-resource. For example, model a sub-collection resource <code>/submissions/12/reviews</code> and add an approval or declination by issuing a <code>POST</code> request. To be able to retrieve the review history (and to consistently adhere to the REST principles), also support the <code>GET</code> method for this resource. The <code>/submissions/12</code> resource might still provide a <code>approved</code> boolean attribute (same as approach 1) which gets automatically updated on the background after adding a review. This attribute should however be read-only.</li>
    <li>In exceptional cases, the approaches above still don't offer an appropriate solution. An example of such an operation is a global search across multiple resources. In this case, the creation of a dedicated resource, possibly nested under an existing resource, is the most obvious solution. Use the imperative mood of a verb, maybe even prefix it with a underscore to distinguish these resources from regular resources. For example: <code>/search</code> or <code>/_search</code>. Depending on the operation characteristics, <code>GET</code> and/or <code>POST</code> method may be supported for such a resource.</li>
  </ol>
  <p>In this design rule, approach 2 and 3 are preferred.</p>
</div>

### Documentation

An API is as good as the accompanying documentation. The documentation has to be easily findable, searchable and publicly accessible. Most developers will first read the documentation before they start implementing. Hiding the technical documentation in PDF documents and/or behind a login creates a barrier for both developers and search engines.

<div class="rule" id="api-08">
  <p class="rulelab"><b>API-08</b>: Use OpenAPI Specification for documentation</p>
  <p><a href="https://www.openapis.org/">The OpenAPI Specification</a> (OAS) defines a standard, language-agnostic interface to RESTful APIs which allows both humans and computers to discover and understand the capabilities of the service without access to source code, documentation, or through network traffic inspection. When properly defined, a consumer can understand and interact with the remote service with a minimal amount of implementation logic.</p>
  <p>API documentation must be provided in the form of an OpenAPI definition document which conforms to the OpenAPI Specification (from v3 onwards). As a result, a variety of tools can be used to render the documentation (e.g. Swagger UI or ReDoc) or automate tasks such as testing or code generation. The OAS document should provide clear descriptions and examples.</p>
</div>

<div class="rule" id="api-09">
  <p class="rulelab"><b>API-09</b>: Publish documentation in English</p>
  <p>In line with design rule <a href="#api-04">API-04</a>, the OAS document (e.g. descriptions and examples) should be written in English.</p>
</div>

<div class="rule" id="api-14">
  <p class="rulelab"><b>API-14</b>: Publish OAS document at a standard location in JSON-format</p>
  <p>To make the OAS document easy to find and to facilitate self-discovering clients, there should be one standard location where the OAS document is available for download. Clients (such as Swagger UI or ReDoc) must be able to retrieve the document without having to authenticate. Furthermore, the CORS policy for this URI must allow external domains to read the documentation from a browser environment.</p>
  <p>The standard location for the OAS document is a URI called <code>openapi.json</code> or <code>openapi.yaml</code> within the base path of the API. This can be convenient, because OAS document updates can easily  become part of the CI/CD process.</p>
  <p>At least the JSON format must be supported. When having multiple (major) versions of an API, every API should provide its own OAS document(s).</p>
  <div class="example">
    <p>An API having base path <code>https://api.example.org/v1/</code> must publish the OAS document at:</p>
    <pre>https://api.example.org/v1/openapi.json</pre>
    <p>Optionally, the same OAS document may be provided in YAML format:</p>
    <pre>https://api.example.org/v1/openapi.yaml</pre>
  </div>
</div>

### Versioning

Changes in APIs are inevitable. APIs should therefore always be versioned, facilitating the transition between changes.

<div class="rule" id="api-18">
  <p class="rulelab"><b>API-18</b>: Adhere to the Semantic Versioning model when releasing API changes</p>
  <p>Version numbering must follow the Semantic Versioning [[SemVer]] model to prevent breaking changes when releasing new API versions. Versions are formatted using the <code>major.minor.patch</code> template. When releasing a new version which contains backwards-incompatible changes, a new major version must be released. Minor and patch releases may only contain backwards compatible changes (e.g. the addition of an endpoint or an optional attribute).</p>
</div>

<div class="rule" id="api-12">
  <p class="rulelab"><b>API-12</b>: Include the major version number in the URI</p>
  <p>The URI of an API (base path) must include the major version number, prefixed by the letter <code>v</code>. This allows the exploration of multiple versions of an API in the browser. The minor and patch version numbers are not part of the URI and may not have any impact on existing client implementations.</p>
  <div class="example">
    <p>An example of a base path for an API with current version 1.0.2:</p>
    <pre>https://api.example.org/v1/</pre>
  </div>
</div>

<div class="rule" id="api-19">
  <p class="rulelab"><b>API-19</b>: Return the full version number in a response header</p>
  <p>Since the URI only contains the major version, it's useful to provide the full version number in the response headers for every API call. This information could then be used for logging, debugging or auditing purposes. In cases where an intermediate networking component returns an error response (e.g. a reverse proxy enforcing access policies), the version number may be omitted.</p>
  <p>The version number must be returned in an HTTP response header named <code>API-Version</code> (case-insensitive) and should not be prefixed.</p>
  <div class="example">
    <p>An example of an API version response header:</p>
    <pre>API-Version: 1.0.2</pre>
  </div>
</div>

<div class="rule" id="api-17">
  <p class="rulelab"><b>API-17</b>: Publish a changelog for API changes between versions</p>
  <p>When releasing new (major, minor or patch) versions, all API changes must be documented properly in a publicly available changelog.</p>
</div>

<div class="rule" id="api-10">
  <p class="rulelab"><b>API-10</b>: Include a deprecation schedule when deprecating features or versions</p>
  <p>Managing change is important. In general, well documented and timely communicated deprecation schedules are the most important for API users. When deprecating features or versions, a deprecation schedule must be published. This document should be published on a public web page. Furthermore, active clients should be informed by e-mail once the schedule has been updated or when versions have reached end-of-life.</p>
</div>

<div class="rule" id="api-11">
  <p class="rulelab"><b>API-11</b>: Schedule a fixed transition period for a new major API version</p>
  <p>When releasing a new major API version, the old version must remain available for a limited and fixed deprecation period. Offering a deprecation period allows clients to carefully plan and execute the migration from the old to the new API version, as long as they do this prior to the end of the deprecation period. A maximum of 2 major API versions may be published concurrently.</p>
</div>

## Examples

To insert (create) a new customer in the system, we might use:
<code> POST <http://www.example.com/customers></code>

To read a customer with Customer ID# 33245:
<code>GET <http://www.example.com/customers/33245></code> The same URI would be used for PUT and DELETE, to update and delete, respectively.

Here are proposed URIs for products:
<code>POST <http://www.example.com/products></code> for creating a new product.

<code>GET|PUT|DELETE <http://www.example.com/products/66432></code>
for reading, updating, deleting product 66432, respectively.

Now, here is where it gets fun... What about creating a new order for a customer? One option might be: <code>POST <http://www.example.com/orders></code> And that could work to create an order, but it's arguably outside the context of a customer.

Because we want to create an order for a customer (note the relationship), this URI perhaps is not as intuitive as it could be. It could be argued that the following URI would offer better clarity: <code>POST <http://www.example.com/customers/33245/orders></code> Now we know we're creating an order for customer ID# 33245.

Now what would the following return?
<code>GET <http://www.example.com/customers/33245/orders></code>
Probably a list of orders that customer #33245 has created or owns. Note: we may choose to not support DELETE or PUT for that url since it's operating on a collection.

Now, to continue the hierarchical concept, what about the following URI?
<code>POST <http://www.example.com/customers/33245/orders/8769/lineitems></code>
That might add a line item to order #8769 (which is for customer #33245). Right! GET for that URI might return all the line items for that order. However, if line items don't make sense only in customer context or also make sense outside the context of a customer, we would offer a <code>POST www.example.com/orders/8769/lineitems</code> URI.

Along those lines, because there may be multiple URIs for a given resource, we might also offer a <code>GET <http://www.example.com/orders/8769></code> URI that supports retrieving an order by number without having to know the customer number.

To go one layer deeper in the hierarchy:
<code>GET <http://www.example.com/customers/33245/orders/8769/lineitems/1></code>
Might return only the first line item in that same order.

By now you can see how the hierarchy concept works. There aren't any hard and fast rules, only make sure the imposed structure makes sense to consumers of your services. As with everything in the craft of Software Development, naming is critical to success.

Look at some widely used APIs to get the hang of this and leverage the intuition of your teammates to refine your API resource URIs. Some example APIs are:

* Twitter: <https://developer.twitter.com/en/docs/api-reference-index>
* Facebook: <https://developers.facebook.com/docs/reference/api/>
* LinkedIn: <https://developer.linkedin.com/apis>

## Glossary

<dl>
  <dt>
    <dfn id="dfn-resource" data-dfn-type="dfn">Resource</dfn>
  </dt>
  <dd>
    <p>A resource is the key abstraction of information, where every piece of information is identified by a globally unique <a href="#dfn-uri">URI</a>.</p>
  </dd>
  <dt>
    <dfn id="dfn-singular-resource" data-dfn-type="dfn">Singular resource</dfn>
  </dt>
  <dd>
    <p>A singular resource is a resource describing a single thing (e.g. a building, person or event).</p>
  </dd>
  <dt>
    <dfn id="dfn-collection-resource" data-dfn-type="dfn">Collection resource</dfn>
  </dt>
  <dd>
    <p>A collection resource is a resource describing multiple things (e.g. a list of buildings).</p>
  </dd>
  <dt>
    <dfn id="dfn-uri" data-dfn-type="dfn">URI</dfn>
  </dt>
  <dd>
    <p>A URI <a href="https://www.ietf.org/rfc/rfc3986.txt">[rfc3986]</a> (Uniform Resource Identifier) is a globally unique identifier for a resource.</p>
  </dd>
</dl>
