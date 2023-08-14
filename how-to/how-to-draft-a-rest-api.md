---
title : How to draft reusable APIs for your businessobjects according to the Synobsys conventions
---
# {{page.title}}

    DRAFT This page is under construction

## Sample Data

In this how to we'll create an xxx REST API for the OutSystems Sample Data

TODO revies this material:

* [REST API Tutorial](https://www.restapitutorial.com/)
* [API Design Cheat Sheet](https://github.com/RestCheatSheet/api-cheat-sheet#api-design-cheat-sheet)
* [Canonical Models Should Be A Core Component Of Your API Strategy](https://github.com/RestCheatSheet/api-cheat-sheet#api-design-cheat-sheet)
* [\[Wikipedia\] Canonical schema pattern](https://en.wikipedia.org/wiki/Canonical_schema_pattern)
* [The Web API Checklist -- 43 Things To Think About When Designing, Testing, and Releasing your API](https://mathieu.fenniak.net/the-api-checklist/)

## Design the API

TODO design canonical schema and api methods.

<https://dzone.com/articles/schema-first-api-design>

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

## Build the API

Because there is no naming convention for rest apis we adhere to the OutSystem
[PascalCase](https://www.theserverside.com/definition/Pascal-case) naming convention

### Build the Canonical schema model

1. Open module  NorthwindSchema_Lib
1. Set the module description to: "Northwind Canonical schema. Provides the canonical structures for use in exposing data with API's"
1. Create a structure for the following exposed entities:
    * Category
    * Customer
    * Employee
    * Order
    * Product
    * Shipper
    * Supplier
1. Steps:
    1. Open the NorthwindDB module.
    1. Select an entity to be exposed e.g. Order.
    1. Copy the Order entity and past it in the library module as a structure
    1. Remove the Id attribute. As a rule we don't expose internal table record id's
    1. There will be errors for all references to other entities resolve this by copying the referenced entity and change the attribute to the coresponding structure. E.g. Order.CustomerId - Customer Identifier -> Order.Customer - Customer structure
1. Set the Public attribute of the structures to Yes.
1. Publish the module
1. To accomodate pagination we need to create a list with count structure so that we can return a page of records and a count of the total available records. Steps:
    1. Create a new "list" structure e.g. ProductsPage
    1. Add a structure attribute Products type product list
    1. Add a structure attribute Count, type LongInteger
    1. Repeat these steps for CustomersPage and OrdersPage
1. Publish the module

### Build the Canonical Business Logic

For each method of the API we must provide a Canonical Business logic server action. This ensures that we don't put business logic in the api implementation and have it available for reuse when exposing other protocols e.g. SOAP.

#### Example retrieve a paged Product list

1. Open the Norhtwind_CBL Module
1. Add a dependency to NorthwindSchemaLib Category, Product and ProductsPage
1. Add a new server action "ProductGet
1. Add the following input parameters:
    * CategoryName, type: text, description: Search on category
    * Search, type: text, description: Search on Name
    * Page, type: Integer, description: Page number for pagination
    * PerPage, type: Integer, description: Number of items per page
1. Add an output parameter result, type ProductsPage
1. Add the following logic:
    * Trim the inputs
    * Validate the inputs
    * Add wildcards to the non empty Search parameter
    * Add an aggregate with Product and Category as sources
    * Filter the aggregate on Category and Search
    * Set Results.Products to the AgregateName.List
    * Set Results.Count to the AggrageteName.Count
    * Convert the aggregate to SQL
    * Add input parameters StartIndex and MaxRecords to the SQL
    * Add an Integer structure to the output of the SQL
    * Append `, COUNT(*), OVER() AS TotalCount` to the select
    * Add the following line to the end of the SQL: `OFFSET @StartIndex ROWS FETCH NEXT @MaxRecords  ROWS ONLY`
    * Set the SQL.StartIndex to (Page-1)*PerPage
    * Set MaxRecords to PerPage
    * Check that the Results output is correct.

### Build the API

1. Install the following forge components:
    * [REST Customized Errors](https://www.outsystems.com/forge/component-overview/15593/rest-customized-errors)
    * ...
1. TODO
