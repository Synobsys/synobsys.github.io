---
title : How to draft reusable APIs for your businessobjects according to the Synobsys conventions
---
# {{page.title}}

## Sample Data

In this how to we'll create an xxx REST API for the OutSystems Sample Data 

TODO revies this material:

* [REST API Tutorial](https://www.restapitutorial.com/)
* [API Design Cheat Sheet](https://github.com/RestCheatSheet/api-cheat-sheet#api-design-cheat-sheet)
* [Canonical Models Should Be A Core Component Of Your API Strategy](https://github.com/RestCheatSheet/api-cheat-sheet#api-design-cheat-sheet)
* [\[Wikipedia\] Canonical schema pattern](https://en.wikipedia.org/wiki/Canonical_schema_pattern)
* [The Web API Checklist -- 43 Things To Think About When Designing, Testing, and Releasing your API](https://mathieu.fenniak.net/the-api-checklist/)

## Design the API with Postman

In this example we'll use Postman API Builder to design the API in Postman

## Setup OutSystems Applications and modules

### Architecture

TODO Insert picture

* Canonical Schema Library: A library containing the canonical schemas used in the apo
* Canonical Business Logic:  A service module exposing Server Actions in canonical schema format.
* API module exposing the REST API

1. Create Application Product API
    1. Open Lifetime (\<your environment \>/lifetime/Applications.aspx )
    1. Click on \[Create Application\]
        * Select the Owner team e.g. Reference Architecture
        * Environment: Development
        * What are you building: Service
        * Name: \[Domain concept API\] (Sample Product API)
        * Description: ?
        * Upload icon: upload an meaninfull icon
        * Create App
    1. Go to Service Studio, wait until the application synchronised from lifetime and open the application
    1. Add Canonical Scheme module
        * Name: SampleProductSchema_Lib
        * Type: Library
        * Set the description to: "Sample Product concept canonical schema."
        * Publish the module
    1. Add Canonical Business Logic CBL Lmodule
        * Name: SampleProduct_CBL
        * Type: Service
        * Set the description to: "SampleProduct Canonical Business Logis (CBL). Provides server actions to be used for exposing data in web services tranforming the Entity records to the canonical schema."
        * Publish the module
    1. Add API Module
        * Name: SampleProduct_API
        * Type: Service
        * Set the description to: "REST API Exposing the sample product concept."
        * Publish the module

TODO
