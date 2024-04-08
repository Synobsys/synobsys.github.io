---
title: Action naming conventions
---
# {{page.title}}

## Server Actions

* Use PascalCase
* Use the \<Verb\>\<Action\> naming pattern for the action name. E.g.: `UserCreate` **not** `CreateUser`
* Prefix actions invoked by Timers with **Timer**
* DON'T use underscores (_) in names. We only have 50 characters for a name.
* Use Entity/Structure names in variables
* Avoid empty labels, for example in in assignments
* Comment unclear or complex logic.
* Set the example string of Expressions.
* Use Static Entities instead of hard-coded values or use one of the [Static entity alternatives].
* Use Site Properties for “semi” static data and secrets

## Service Action naming conventions

Service actions are also known as **O**utSystems **API**s (OAPI)

* Service Actions follow the Server Action naming with version suffix
* Versioning
    * Only use major versions, starting at **V1**.
    * Versions are reflected in the name of the Service Action. E.g. 'CustomerGetV1'
    * Only backwards INcompatible updates lead to a new version of the OAPI.
* Don't use underscores in names

Example: **CustomerCreateV1**

## Client Action naming

1. Follow the same rules as server actions

## Screen Action naming

* Use PascalCase
* Use On\<action\> e.g. 'OnSort', 'OnSave', 'OnCustomerSelected'

[Static Entity Alternatives]: how-to\static-entity-alternatives.md
