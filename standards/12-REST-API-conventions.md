# REST API conventions

## Abstract

TODO

* Eigenschappen van een REST API
* Anatomie van een OpenAPI Specificatie
* Wanneer maak je een API?
* Hoe bepaal je de scope en het doel van de API?
* Resource en proces operaties
* Chaining
* API Conventies
* API of messaging
* Design van events en callbacks
* Case study: Connections API
* Design authority

## How to draft reusable APIs for your businessobjects according to ths Synobsys conventions

## Properties of a REST API

### Synchronous communication

* OpenAPI Spec (and HTTP) require a response
* Consumer initiates the interaction with a request
* The response does not have to mean that the request is fully processed
* With a success response, the producer is responsible for any further processing, with an error response, the consumer remains responsible

### Standard (HTTP) operations

* Primair resource- and not action-oriented (such as SOAP/RPC)
* Avoid verbs in the API: that's what the standard operations are for
* Client needs to implement more logic
* The starting point is two base URLs per resource: collection and object

Example: User

| Resource | POST (Create) | GET (Read) | PUT(Update) | DELETE (delete) | PATCH (Update) |
| -------- | ------------- | ---------- | ----------- | --------------- | -------------- |
| /users | Create a new user | List all users | ~~Replace all users~~ | ~~Delete all users~~ | ~~Update specific attributes of all users~~ |
| /user/123 | ~~Create user with ID 123~~ | Return user 123 | If user 123 exists then update else create | Delete user 123 | Update specific attributes of user 123 |

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
