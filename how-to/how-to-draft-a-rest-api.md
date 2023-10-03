---
title : How to draft reusable APIs for your businessobjects according to the Synobsys conventions
---
# {{page.title}}

    🏗️ DRAFT This page is under construction 

## Northwind data

In this how to we'll create an ProductOrdering REST API for the [Northwind](https://www.outsystems.com/forge/component-overview/4152/northwind) forge component.

    TODO review this material:

* [REST API Tutorial](https://www.restapitutorial.com/)
* [API Design Cheat Sheet](https://github.com/RestCheatSheet/api-cheat-sheet#api-design-cheat-sheet)
* [Canonical Models Should Be A Core Component Of Your API Strategy](https://github.com/RestCheatSheet/api-cheat-sheet#api-design-cheat-sheet)
* [\[Wikipedia\] Canonical schema pattern](https://en.wikipedia.org/wiki/Canonical_schema_pattern)
* [The Web API Checklist -- 43 Things To Think About When Designing, Testing, and Releasing your API](https://mathieu.fenniak.net/the-api-checklist/)
* [Securing Your OutSystems APIs
With OAuth 2.0](https://www.outsystems.com/blog/posts/securing-outsystems-apis-oauth2/)
* [Exposing an OutSystems REST service with an OAuth-style authorization](https://itnext.io/exposing-an-outsystems-rest-service-with-an-oauth-style-authorization-fded258cbe14)
* [Protect OutSystems REST APIs using OpenID Connect](https://medium.com/itnext/protect-outsystems-rest-apis-using-openid-connect-87a2ac7575c1)

## Design the API

* [ ] TODO design canonical schema and api methods see <https://dzone.com/articles/schema-first-api-design>

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
    * Add a seperate count aggregate and minimize the joins.
    * Add the following line to the end of the SQL: `OFFSET @StartIndex ROWS FETCH NEXT @MaxRecords  ROWS ONLY`
    * Set the SQL.StartIndex to (Page-1)*PerPage
    * Set MaxRecords to PerPage
    * Check that the Results output is correct.

### Build the API

1. Install required forge components
    * [REST Customized Errors](https://www.outsystems.com/forge/component-overview/15593/rest-customized-errors)
    * ...

1. Define the API and methods

    1. In service studio open module `ProductOrderingAPI`
    1. Open the logic tab `<Ctrl_3>`
    1. Expand `Integrations`
    1. Right click on REST and select `Expose REST API`

        * Name: V1
        * Description: Product Ordering API Version 1
        * Authentication: Basic see [how to Add Custom Authentication to an Exposed REST API](/how-to/how-to-add-custom-authentication-to-an-exposed-rest-api.md) for other authentication methods.
        * OnResponse : New OnResponse
    1. Add the following logic to the OnResponse action
        * REST_CustomErrors_Lib/REST_CustomizeResponse
        * Assign CustomizedResponse = REST_CustomizeResponse.CustomizedResponse
        * AddHeader Name: Version Value: "1.0.0"
    1. Right click on `V1` and select Add REST API Method

        * Name: CategoriesGet
        * Input parameters: none
        * Output parameters: categories (Category list)
        * Description: Returns a list of categories.
        * URL Path: /categories
        * HTTP Method: GET
    1. Repeat this step for each of the following methods:

        | Name | Inputs | Output | Description | URL Path | Method |
        | ---- | ------ | ------ | ----------- | -------- | ------ |
        | CustomerGetById | customer_id | customer |Returns the customer details for a given customer. | /customers/{customer_id} | GET |
        | CustomerCreate | customer | customer_id | Creates a new customer | /customers | POST |
        | CustomerDelete | customer_id | - | Deletes a specific customer | /customers/{customer_id} | DELETE |
        | CustomersGet | - | customers | Retrieves a list of customers | /customers | GET |
        | CustomerUpdate | customer | - | Updates a customer | /customers | PUT |
        | OrderCreate | order | order_id | Place an order | /orders | POST |
        | OrderGetById | order_id | order | Return the details of a specific order | /orders/{order_id}| GET |
        | OrdersGet | page, per_page | orders | Retrieve a paginated list of orders | /orders | GET |
        | CustomerOrdersGet | customer_id, status, page, per_page | orders | Retrieves a list of orders for a specific customer | /customers//customers/{customer_id}/orders | GET |
        | ProductsGet | category, search, per_page, page | products | Retrieve a paginated list of products that meet the search parameters. | /products | GET|
        | ProductGetById | product_id | product | Retrieve details of a specific product | /products/{product_id} | GET |

    TODO [Appropriate record counting](https://success.outsystems.com/documentation/11/managing_the_applications_lifecycle/manage_technical_debt/code_analysis_patterns/appropriate_record_counting/)

    TODO
