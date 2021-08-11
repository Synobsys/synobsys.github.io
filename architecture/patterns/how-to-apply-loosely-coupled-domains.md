---
title: How-to apply loosely coupled domains
---
# How-to apply loosely coupled domains

This how-to explains how to apply a strict loosely coupled domain architecture

## Rules

Across domains, keep loose coupling relationships, providing domain APIs divided in two parts:

* **Public structures**

Canonical structures to provide normalized structures

* **Service actions**

Data transactions and detail retrieval

* Until there is a performance requirement we will **not** use public entities

## Domain architecture

To provide a clear separation between intra- and extra domain logic use the following application architecture.

* \<domain\> Canonical Library - providing the canonical structures. Containing the following modules:
    * \<DomainPrefix\>\<conceptname\>_Lib - Library modules containing the canonical model
    * \<domain\> Core - providing core services
    * \<domain\> UI - domain user interface modules
    * \<domain\> OAPI - providing Service Actions

## Example Domain Architecture

Domain | Acronym | Concepts
---|---|---
**Party** | PTY | Customer
-|-| Shipper
-|-| Supplier
**Product**| PRD|Products
**Sales**|SLS|Sales Orders
**Organization**|ORG|Employees

### Party applications and modules

Application | Module | Layer
--- | --- | ---
PTY Party UI (private)| Customers
-| Suppliers
-| Shippers
PTY Party Core (private) | PTY_Customer_CS
-| PTY_Customer_CBL
-| PTY_Employee_CS
-| PTY_Employee_CBL
-| PTY_Shipper_CS
-| PTY_Shipper_CBL
-| PTY_Supplier_CS
-| PTY_Supplier_CBL
PTY Party Library - shared| PTY_Customer_Lib
-| PTY_Employee_Lib
-| * ...
PTY Party OAPI - shared| PTY_Customer_OAPI
-| PTY_Employee_OAPI
-| * ...
PTY Party API - shared | Not implemented

### Product applications ans modules

Application|Module
---|---
PRD Product Core | PRD_Product_CS
PRD Product OAPI | PRD_Product_OAPI
