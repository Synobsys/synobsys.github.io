---
title: Module naming conventions
---
# Module naming conventions

* TOC
{:toc}

* Use **PascalCase** and don't use underscores except for the layer Suffix or Prefix.
* Prefix the module name with the Application acronym except for end user modules. (The module name is part of the url and we should not bother users with technicalities.)

## Core Layer Module Naming

Reusable services around business concepts, exporting entities, business rules and web-blocks

| Layer | SubLayer | Suffix | Description                                  | Example |
| --- | --- | ----- | ---------------------------------------------- | ------|
| Core Modules | API | _API    | Wrapper that expose an **API** for External consumers (REST/SOAP) to the OutSystems platform, supporting multiple versions.| Pricing_API|
| | | _OAPI | Wrapper that exposes an **API** for internal consumers(Service Actions) (**O**utSystem **API**) to Internal Consumers, keeping core services system agnostic and supporting multiple versions of the API| Pricing_OAPI|
| | Core Widgets| _CW,_MCW | Isolated **C**ore **W**idgets (Blocks), to manage complexity, composition or to have its own lifecycle | Customer_CW |
| | Composite logic | _BL, MBL | Isolated **B**usiness **L**ogic (Actions) to manage complexity, composition or to have its own lifecycle | Pricing_BL |
| | | _Eng | A BL becomes a Calculation **Eng**ine if it performs complex calculations, (e.g. an invoice calculation engine or an insurance simulator). **Eng**ines are usually subject to versions | Pricing_Eng |
| | | _Sync | Logic to **Sync**hronize data in CSs with an external system. Isolating this logic makes the CS completely system agnostic and it’s easier to decouple or replace the external system | Field_Sync |
| | Core Services | _CS,_MCS |  Reusable **C**ore **S**ervices with public entities, actions and web blocks | Customer_CS, Field_CS, SupplierAudit_CS, StoreAudit_CS |

Note: *An “M” indicates a Mobile only module, like _MCS, _MBL or _MCW*

## Foundation Layer Module Naming

Non Functional requirements or integration modules, reusable in any business context

| Sub-layer | Prefix | Description                                    | Example |
| ---| ------ | ---------------------------------------------- | ------- |
| Style guide | _Pat,_MPat | Reusable UI **Pat**terns for layout and display only - no Business logic | UserExtension_Pat, Backoffice_Pat |
| | _Th | **Th**eme, look & feel elements, menu, ... |Internal_Th, Supplier_Th, Backoffice_Th |
| |Template_ |Theme **templates** | Template_Backoffice, Template_Internal|
|Foundation Services | _IS | **I**ntegration **S**ervices - technical wrapper to consume and normalize an external service | SoccerField_IS |
| | _FS | **F**oundations **S**ervices to support NFR's (e.g. Audit trailing) | |
| | _Drv | **Dr**i**v**er module - to have several integration services with different systems, performing the same type of operation (e.g. printers) you can create several drivers exposing the same API, with specialized implementations (like the transparency services pattern) | |
| | _Lib | A generic module of type **Lib**rary | CipherUtils_Lib |

*An “M” indicates a Mobile only module, like _MPat,*

---

## Soccer Fields naming example

| Type   | Name          | Acronym |
| ------ | --------------| --- |
| Domain | Soccer Fields | SF |
| Application | SF Soccer Fields App | SF |
| Application | SF Field Core Services | FLC |
| Application | SF Soccer Fields Core | SFC |
| Module | SoccerFields | |
| Module | SF_Th | |
| Module | SFC_Booking_CS | |
| Module | SFC_Player_CS | |
| Module | FLC_Field_CS | |
| Module | FLC_Field_IS | |
| Module | FLC_Field_Sync | |

## Reference

Review the following OutSystems documentation on module types:

* [Service Modules and Service Applications]
* [Libraries]

[Service Modules and Service Applications]: https://success.outsystems.com/documentation/11/building_apps/reusing_and_refactoring/use_services_to_expose_functionality/#service-modules-and-service-applications
[Libraries]: https://success.outsystems.com/documentation/11/building_apps/reusing_and_refactoring/libraries/