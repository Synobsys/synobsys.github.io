---
Title: OutSystems Naming Conventions
---

# OutSystems Naming Conventions

## Table of contents

1. [Language](#language)
1. [Domains](Naming\domain-naming.md)
1. [Applications](Naming\application-naming.md)
1. [Modules](Naming\module-naming.md)
1. [Entities and attributes](Naming\enitity-naming.md)
1. [Variables](#variables)
1. [Screens](#screens)
1. [Blocks](#blocks)
1. [Actions](#actions)
1. [Service Actions (OutSystems APIs)](#service-actions)
1. [REST APIs](#rest-apis)
1. [SOAP Services](#soap-services)
1. [CSS](#css)
1. [Test Code naming](#test-code-naming)

---

    TODO Issue #4 ADR and Template for Common Glossary

## Language

* All OutSystems code (Service Studio and Integration Studio), including comments and documentation will be in English. [ADR-002](adr\ADR-002-standard-language-is-English.md)
* Business terms in the OutSystems model will be in English and be taken from the **Common Glossary**.

* All UI in the OutSystems model will be developed in English and may be translated using the standard OutSystems localization features if required.
* Objects in the OutSystems environment have meaningful, unabbreviated names. Where naming limits prevent this (most OutSystems element names have a limit of 50 characters), standard abbreviations as provided in the **Common Glossary** must be used.

---

## Variables

Local variables used as constants (i.e. have a fixed, default value that is not supposed to be changed over their lifetime) have a meaningful name, prefixed by the word `Const` (e.g. `ConstPollingInterval`)

---

## Screens

* Screen names start with the name of the (main) entity followed by a suffixes showing the purpose of the screen names. Use the following suffixes:
    * _List - Listing instances e.g. `Customer_List`
    * _Edit - for editing a record e.g. `Customer_Edit`
    * _Show - showing a record e.g. `Customer_Show`
    * tbd add more suffixes

* Set the name property of ShowRecords, EditRecords and TableRecords *TBD include reactive variant*
* Action button text is specified on UX design and follows UX standards. In situations where no UX design is available, the following action button text applies:
    * ‘Save’ to trigger the action to store the data of the current instance of an entity in the database
    * ‘Back’ to cancel the action and return to the previous screen
    * ‘New” to start the creation of a new instance of an entity
    * ‘Delete’ to (logically) remove the current instance from the database
    * ‘Edit’ to start editing the current instance on an entity

---

## Blocks

* Reusable (web-)blocks have a name that describes their function followed by the suffix `_Block` e.g `Customer_Block`

---

## Actions

* *tbd check for completeness*

* Prefix actions invoked by Timers with `Timer_`
* Use Entity/Structure names in variables
* Avoid empty labels, for example in in assigments
* Comment unclear or complex logic.
* Set the example string of Expressions
* Use Static Entities instead of hard-coded values
* Use Site Properties for “semi” static data
* Use Pascal Case

---

## Service Actions

Service actions are also known as **O**utSystems **API**s
TBD *Should we adopt a similar naming as for REST APIs?*

1. Service Actions follow the Server Action naming with the suffix "SA"
1. Versioning
    * Only use major versions, starting at v1.
    * Versions are reflected in the name of the Service Action.
    * Only backwards INcompatible updates lead to a new version of the API.
1. Don't use underscores in names

Example: `CustomerCreateSAv1`

---

## REST APIs

There will be multiple APIs and potentially multiple versions of the same API. This requires naming conventions and logical structuring.

1. Base paths are based on resources.

```
/users              -&gt; retrieves all users.
/users/{userId}     -&gt; retrieves a specific user.
```

1. Resource names are plural nouns like "users", "customers" etc.
1. Path parameters and query parameters are implemented correctly
1. When fetching an object by ID, the parameter should be in the path.
Example(s):     `/v1/customers/123`

1. When searching through a list of objects, the parameters should be in the query:
Example(s):     `/v1/customers?name=Appy&status=active`
1. API Versioning

* Only use major versions, starting at v1.

* Versions are reflected in the path of the API.
* Only backwards INcompatible updates lead to a new version of the API.

1. Words and field names are in camelCase
Note: This is an exception to the OutSystems rule that names are in PascalCase.

```
{
    "customerNumber": 12345,
    "customerGroup": "internal"
}
```

---

## SOAP Services

The rules for SOAP services have not yet been established.

---

## CSS

For CSS naming in OutSystem we use a slightly modified BEM (Block, Element, Modifier).
See <http://getbem.com/naming/> Note: Do not use underscores “__” in the names.
Block is the entire component e.g. .card and should be considered as a parent. E.g.

* `.card-title{}`
* `.card-content{}`
* `.card-footer{}`

Naming rules:

* All CSS must be in lowercase
* Separate names with a hyphen. e.g. `.color-red`
* Use tab to indent the declarations
* Write your rules in alphabetical order
* Selectors must be separated by a new line
* Use shorthand when possible e.g. `padding: 10px;`
* Do not use units when using zeroes. E.g. `padding: 0;`
* Also leave out the 0 before the pivot. E.g. `opacity: .7;`
* Be aware when vendor prefixes are required (`-webkit-transform`)

## Test Code naming

Test Applications
: &lt;Lifetime Application name&gt; Tests

Test modules
: &lt;Feature/Concept/Goal&gt;_Tests

Test Data modules
: &lt;Domain/Subdomain/Concept&gt;_TestDataSetup

Shared Pattern Modules
: &lt;Domain/Subdomain/Concept&gt;_TestDataShared

Test screens
: &lt;Concept/Goal&gt;_TestSuite

Test Blocks
: &lt;Concept/Goal&gt;_Test

Test Data actions
: &lt;Concept&gt;_&lt;RecordName&gt;_Get
: &lt;Concept&gt;_&lt;RecordName&gt;_Create
: &lt;Concept&gt;_&lt;RecordName&gt;_Teardown
