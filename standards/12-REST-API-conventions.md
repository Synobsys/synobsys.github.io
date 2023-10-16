---
title : REST API conventions
---
# {{page.title}}

## Contents

* TOC
{:toc}

TODO:

* [ ] When to expose an API?
* [ ] How to determine the scope and the purpose of the API?
* [ ] Resource and proces operations
* [ ] Chaining
* [ ] API Conventions
* [ ] API of messaging
* [ ] Design of events and callbacks
* [ ] Design authority

## Properties of a REST API

### Synchronous communication

* OpenAPI Spec (and HTTP) require a response
* Consumer initiates the interaction with a request
* The response does not have to mean that the request is fully processed
* With a success response, the producer is responsible for any further processing, with an error response, the consumer remains responsible

## API design rules

### Standard (HTTP) operations

Use HTTP verbs to operate on the collections and elements.

* Primair resource- and not action-oriented (such as SOAP/RPC)
* Avoid verbs in the API: that's what the standard operations are for
* Client needs to implement more logic
* The starting point is two base URLs per resource: collection and object

Example: Dog

| Resource | POST (Create) | GET (Read) | PUT(Update) | DELETE (delete) | PATCH (Update) |
| -------- | ------------- | ---------- | ----------- | --------------- | -------------- |
| `/dogs` | Create a new dog | List dogs | Bulk update dogs | Delete all dogs | Update specific attributes of all dogs |
| `/dogs/123` | Error | Show Bo | If exist update Bo <br> If not Error | Delete Bo | Update specific attributes of Bo |

### Plural nouns and concrete names

Given that the first thing most people probably do with a RESTful API is a GET, we think it reads more easily and is more intuitive to use plural nouns.

### Simplify associations - sweep complexity under the ‘?’

Most APIs have intricacies beyond the base level of a resource. Complexities can include many states that can be updated, changed, queried, as well as the attributes associated with a resource.
Make it simple for developers to use the base URL by putting optional states and attributes behind the HTTP question mark. To get all red dogs running in the park:

`GET /dogs?color=red&state=running&location=park`

In summary, keep your API intuitive by simplifying the associations between resources, and sweeping parameters and other complexities under the rug of the HTTP question mark.

### Handling errors

#### How many status codes should you use for your API?

When you boil it down, there are really only 3 outcomes in the interaction between an app and an API:

* Everything worked - success
* The application did something wrong – client error
* The API did something wrong – server error

Start by using the following 3 codes. If you need more, add them. But you shouldn't need to go beyond 8.

* 200 - OK
* 400 - Bad Request
* 500 - Internal Server Error

If you're not comfortable reducing all your error conditions to these 3, try picking among these additional 5:

* 201 - Created
* 304 - Not Modified
* 404 – Not Found
* 401 - Unauthorized
* 403 - Forbidden

#### Make messages returned in the payload as verbose as possible.

Code for code

* 200 – OK
* 401 – Unauthorized

Message for people

```json
{"developerMessage" : "Verbose, plain language description of the problem for the app developer with hints about how to fix it.", 
"userMessage":"Pass this message on to the app user if needed.", 
"errorCode" : 12345, 
"more info": "http://dev.teachdogrest.com/errors/12345"}
```

You can use the [REST Customized Errors](https://www.outsystems.com/forge/component-overview/15593/rest-customized-errors) forge component to create these messages.

### Versioning

Versioning is one of the most important considerations when designing your Web API.

**Never release an API without a version and make the version mandatory.**

Specify the version with a 'v' prefix. Move it all the way to the left in the URL so that it has the highest scope (e.g. `/v1/dogs`).

Use a simple ordinal number. Don't use the dot notation like v1.2 because it implies a granularity of versioning that doesn't work well with APIs--it's an interface not an implementation. Stick with v1, v2, and so on.

#### How many versions should you maintain?

Maintain at least one version back.

#### For how long should you maintain a version?

Give developers at least one cycle to react before obsoleting a version.

Sometimes that's 6 months; sometimes it’s 2 years. It depends on your developers' development platform, application type, and application users. For example, mobile apps take longer to rev’ than Web apps.

### Pagination and partial response

Partial response allows you to give developers just the information they need.
Take for example a request for a tweet on the Twitter API. You'll get much more than a typical twitter app often needs - including the name of person, the text of the tweet, a timestamp, how often the message was re-tweeted, and a lot of metadata.

#### Add optional fields in a comma-delimited list

Here's how to get just the information we need from our dogs API using this approach:
`/dogs?fields=name,color,location`

It's simple to read; a developer can select just the information an app needs at a given time; it cuts down on bandwidth issues, which is important for mobile apps.

#### Make it easy for developers to paginate objects in a database

It's almost always a bad idea to return every resource in a database.
Use limit and offset
We recommend limit and offset. It is more common, well understood in leading databases, and easy for developers.

To get records 50 through 75 , you would use:

`/dogs?limit=25&offset=50`

### Tips for search

While a simple search could be modeled as a resourceful API (for example, `dogs/?q=red`), a more complex search across multiple resources requires a different design.

This will sound familiar if you've read the topic about using verbs not nouns when results don't return a resource from the database - rather the result is some action or calculation.

If you want to do a global search across resources, we suggest you follow the Google model:

#### Global search

`/search?q=fluffy+fur`

Here, search is the verb; `?q` represents the query.

#### Scoped search

To add scope to your search, you can prepend with the scope of the search. For example, search in dogs owned by resource ID 5678

`/owners/5678/dogs?q=fluffy+fur`

### Authentication

Authentication methods:

* Basic - UserId and Password
* Custom using an API Key
* Custom using an Authorisation token e.g. JWT, OpenId etc. see [Protect OutSystems REST APIs using OpenID Connect](https://itnext.io/protect-outsystems-rest-apis-using-openid-connect-87a2ac7575c1)

#### Custom authenthication with an API Key

Following the steps described in [Add Custom Authentication to an Exposed REST API](https://success.outsystems.com/documentation/11/extensibility_and_integration/rest/expose_rest_apis/add_custom_authentication_to_an_exposed_rest_api/) we will implement authentication using an API Key.

## References

* <https://www.outsystems.com/blog/posts/implementing-http-status-code-exposing-rest/>
* <https://www.outsystems.com/forge/component-overview/5547/rest-http-codes>

## Tools

### VisualStudio Code

* <https://marketplace.visualstudio.com/items?itemName=42Crunch.vscode-openapi>
* <https://marketplace.visualstudio.com/items?itemName=Arjun.swagger-viewer>

### NPM

<https://www.npmjs.com/package/swagger-cli>

npm i swagger-cli@2.3.5 –g (dus niet laatste versie gebruiken)

### Swagger IO

<https://editor.swagger.io/>

### Open API Specification

<http://spec.openapis.org/oas/v3.0.3>
