---
title: How-to add an entity to your module
---

# {{page.title}}

The standards require entities to be exposed read only. Therefore we require public database actions (aka crud wrappers).
Follow this guideline to setup the database actions.

* TOC
{:toc}

## Instal Forge components

Install the latest version of the [CRUD wrappers stencils](https://www.outsystems.com/forge/component-overview/13991/crud-wrappers-stencils) forge component

## Setup security

1. Identify the role that that has permissions to modify the entity. E.g. FieldsAdmin
1. In the **\<domain\>_security_lib** check if the role and the **\<yourrole\>Check** action exist.
1. If the role does not exist
    * add **\<YourRole\>** in the security module
    * create a **\<YourRole\>Check** Server Action
    * make both the role and the service action public
1. Open de dependencies in **\<your core services module\>** and add a dependency to the **\<YourRole\>** and **\<YourRole\>Check** action

## Creating a new entity

 > :warning: **WARNING:** Do **NOT** publish the module before it is indicated!

1. In ServiceStudio open **\<YourCoreServices\>** module
1. With \<Ctrl+O\> open the **Stencil_DBActions_Pat** module
1. Go to the Stencil_DBActions_Pat data tab \<Ctrl+4\>
1. Copy **TemplateEntity** to your module
1. Rename **TemplateEntity** to the **\<new entity name\>**
1. Change the **Expose Read Only** property to **Yes**
1. Open the entity editor and enter a proper description for the entity
1. In the entity editor open the More options and set the
    * Label
    * Label (plural)
    * Order by attribute
1. Check that the entity and all the attributes have proper descriptions.

## Add database actions for the new entity

1. Switch to the **Stencil_DBActions_Pat** and go to Logic tab (Ctrl-3)
1. Make sure the folder **TemplateEntityDbActions** is collapsed
1. Copy folder **TemplateEntityDbActions** and Paste it in **\<your core services module\>** logic tab
1. Go to Data tab (Ctrl-4) and locate the **TemplateEntity** in the **Stencil_DBActions_Pat** referenced module
1. Find all usages of the **TemplateEntity** (F12)
1. Use the button: **Replace all instances** to replace with your new entity (select in the popup)
1. Remove the TemplateEntity dependency (Del)
1. Using (Ctrl + R): find string "TemplateEntity" and replace all occurrences with your new entity

## Rename the natural key attribute

A natural key (also known as business key or domain key) is a type of unique key in a database formed of one or more attributes that exist and are used in the external world outside the database (i.e. in the business domain or domain of discourse). In the relational model of data, a natural key is a super key and is therefore a functional determinant for all attributes in a relation. From [Wikipedia: Natural Key]

1. Designate a meaningful name to the Natural Key for your entity and using (Ctrl + R) find string "NaturalKey"and replace all occurrences with that name.
1. Fix the errors one by one by clicking on each of them.
1. If the natural key is a composed of multiple attributes change the \<Natural key attribute\> index and the validation actions accordingly.
1. When done, check all the TBD (To Be Done) items (shown as warnings in the TrueChange tab) and remove them when OK
1. Check that there are no warnings in the TrueChange tab
1. 1-Click publish your module.

## Create BDD tests

Now follow the [how to create entity BDD tests](/how-to/how-to-create-entity-bdd-tests-from-a-stencil.md) to create the test functionality.

[Wikipedia: Natural Key]: https://en.wikipedia.org/wiki/Natural_key
