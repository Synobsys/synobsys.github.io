---
title: Action naming conventions
---
# {{page.title}}

    TODO check for completeness

## Server Actions

* Use PascalCase
* Use the \<Verb\>\<Action\> naming pattern for the action name. E.g.: UserCreate
* Prefix actions invoked by Timers with **Timer**
* DON'T use underscores (_) in names. We only have 50 characters for a name.
* Use Entity/Structure names in variables

    TODO Move to coding style guide

* Avoid empty labels, for example in in assignments
* Comment unclear or complex logic.
* Set the example string of Expressions
* Use Static Entities instead of hard-coded values
* Use Site Properties for “semi” static data

## Service Action naming conventions

Service actions are also known as **O**utSystems **API**s (OAPI)

* Service Actions follow the Server Action naming with the suffix "SA"
* Versioning
    * Only use major versions, starting at **_v1**.
    * Versions are reflected in the name of the Service Action.
    * Only backwards INcompatible updates lead to a new version of the API.
* Don't use underscores in names

Example: **CustomerCreateSAv1**

## Client Action naming

1. Follow the same rules as server actions

## Screen Action naming

* Use PascalCase
* Use On\<action\> e.g. OnSort, OnSave, OnCustemerSelected
