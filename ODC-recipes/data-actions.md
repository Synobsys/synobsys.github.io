---
title: ODC Recipe - Create an Entity and Data Actions
---
# {{page.title}}

A data action is a piece of logic that performs a create update or delete action on one or more entities.

## Exposing data with ODC

Contrary to O11 in ODC entities are always exposed read only and server actions are not public.

The rule is to expose entities read only and to use Service Actions to expose the CRUD operations.

## CRUD Templates

We use the CRUD templates application from the forge to speed up and standardize the creation of Entities and Data Actions.

The template has the following elements:

### Template Entity

![Template Entity](/ODC-recipes/images/TemplateEntity.png)

The template entity has the following attributes:

### Id

A generated [UUIDv7] primary key

* [ ] TODO replace GenerateGuid() with UUID7 available on 21-11-2023.

### NaturalKey

A natural key is an attribute that exists in the real world or is used by the business. It can be used to uniquely identify the row.
An example of a natural key is a Social Security Number (for US citizens). It’s usually a unique number that applies to a person, and has a use for tax purposes.

### Description

A text attribute describing the entity instance

### Audit fields

* CreatedByUserId - UserId
* CreatedOn - DateTime
* UpdatedByUserId - UserId
* UpdatedOn - DateTime

### Unique NaturalKey index

An index to ensure the uniqueness of the natural key.

## TemplateEntityDbActions

* TemplateEntity_CreateOrUpdate - Create or update a valid record.
* TemplateEntity_Delete - Delete a TemplateEntity record
* TemplateEntity_Validate - Performs the TemplateEntity record validation

## Utility Actions

You may want to put these actions in a library for reuse.

* NotificationListConcat - Concatenates a list of notifications to one string using StringBuilder.

## Adding a new entity and data actions to an application

### Preparation

1. If not already present, add the **CRUD Templates** application from the forge.
1. If not present copy the [Utility Actions](#utility-actions) to your application or library
1. Determine the role that is authorized to perform the data actions and create it in **\<Your Application\>**
1. Add a **ValidationException** to **\<Your Application\>**
1. Add a **ConcurrentUpdateException** to **\<Your Application\>**

### Creating the new Entity

:warning: **WARNING**:  Do **NOT** publish the application before instructed to do so.

1. Open **\<Your Application\>**
1. Open the **CRUD Templates** application
1. Go to the data tab (Ctrl+4)
1. Select **TemplateEntity** and copy it
1. Switch to **\<Your Application\>** and paste the **TemplateEntity**
1. Rename **TemplateEntity** to the **\<new entity name\>**
1. Open the entity editor and enter a proper description for the entity.
1. In the entity editor open the More options and set the:
    * Label
    * Label (plural)
    * Order by attribute
1. Check that the entity and all the attributes have proper descriptions.

### Add database actions for the new entity

1. Switch to the **CRUD Templates** and go to Logic tab (Ctrl-3)
1. Make sure the folder **TemplateEntityDbActions** is collapsed
1. Copy folder **TemplateEntityDbActions** and Paste it in **\<Your Application\>** logic tab
1. Go to Data tab (Ctrl-4) and locate the **TemplateEntity** in the **Stencil_DBActions_Pat** referenced module
1. Find all usages of the **TemplateEntity** (F12)
1. Use the button: **Replace all instances** to replace with your new entity (select in the popup)
1. Remove the TemplateEntity dependency (Del)
1. Using (Ctrl + R): find string "TemplateEntity" and replace all occurrences with your **\<new entity name\>**
1. Using (Ctrl + R): find string "TemplateEntities" and replace all occurrences with your **\<new entity name\>** plural form. E.g. Products.
1. Fix the errors by replacing the missing entity actions with **\<new entity name\>** entity actions and the exceptions;
    * 'GetTemplateEntityForUpdate'
    * 'CreateTemplateEntity'
    * 'DeleteTemplateEntity'
    * 'UpdateTemplateEntity'
    * ValidationException
    * ConcurrentUpdateException
1. Remove all the TODO Reminder comments when they are done.

### Rename the natural key attribute

A natural key (also known as business key or domain key) is a type of unique key in a database formed of one or more attributes that exist and are used in the external world outside the database (i.e. in the business domain or domain of discourse). In the relational model of data, a natural key is a super key and is therefore a functional determinant for all attributes in a relation. From Wikipedia [Natural Key]

1. Designate a meaningful name to the [Natural Key] for your entity and using (Ctrl + R) find string "NaturalKey"and replace all occurrences with that name.
1. Fix the errors one by one by clicking on each of them.
1. If the natural key is a composed of multiple attributes change the \<UniqueNaturalKey\> index and the validation actions accordingly.
1. When done, check all the Reminder TODO comments (shown as warnings in the TrueChange tab) and remove them when OK.
1. Check that there are no warnings in the TrueChange tab

### Add additional attributes

1. Add any additional attributes and set the properties:
    * Name
    * Description
    * Data Type
    * Is Mandatory
1. Add validation logic for each new attribute in the Validate server action.
1. 1-Click publish your module.

## Exposing Data Actions

If there is a requirement to modify the data from within another domain or application you can expose the data actions as service actions or as an API.

### Creating Data structures

For external resources we don't want to expose the full entity record. Therefore we create a so called canonical data structure.

1. Open the data tab (Ctrl+4) and select and copy **\<new entity name\>**
1. Paste it inside the Structures Tab
1. Rename the structure to **\<new entity name\>**CS (Canonical Structure)

[UUIDv7]: https://uuid7.com/
[Natural Key]: https://en.wikipedia.org/wiki/Natural_key
