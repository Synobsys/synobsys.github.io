---
title: ODC Recipe - Create an Entity and Data Actions
---
# {{page.title}}

A data action is a piece of logic that performs a create update or delete action on one or more entities.

## Contents

* TOC
{:toc}

## Exposing data with ODC

Contrary to O11 in ODC entities are always exposed read only and server actions are not public.

The rule is to expose entities read only and to use Service Actions to expose the CRUD operations.

## CRUD Templates

We use the CRUD templates application from the forge to speed up and standardize the creation of Entities and Data Actions.

The template has the following elements:

### Template Entity

![Template Entity](/ODC-recipes/images/TemplateEntity.png)

The template entity has the following attributes:

| Attribute | Description |
| --- | --- |
| Id | A generated [UUIDv7] primary key (TODO replace GenerateGuid() with UUID7 available on 21-11-2023.) [Why Auto Increment Is A Terrible Idea] describes why we chose UUID in favor of Auto Increment.See also [Primary Keys: IDs versus GUIDs]|
| NaturalKey | A [natural key] is an attribute that exists in the real world or is used by the business. It can be used to uniquely identify the row. An example of a natural key is a Social Security Number (for US citizens). It’s usually a unique number that applies to a person, and has a use for tax purposes. |
| Description | A text attribute describing the entity instance |
| CreatedByUserId | The Id of the user who created the record. |
| CreatedOn | DateTime the record was created |
| UpdatedByUserId | The Id of the user who updated the record. |
| UpdatedOn | DateTime the record was updated. We use this attribute to handle concurrent updates as described in [How To Handle Concurrent Updates on Application Data Records] |

### Unique NaturalKey index

An index to ensure the uniqueness of the natural key.

### TemplateEntityDbActions

* TemplateEntityCreateOrUpdate - Create or update a valid record.
* TemplateEntityDelete - Delete a TemplateEntity record
* TemplateEntityValidate - Performs the TemplateEntity record validation
* TemplateEntityForgeUpdate - Forges the update of a record overwriting a previous update

:warning: **WARNING** There is no Login server action. All background processes such as timers and bpt run without a session and user. The CheckRole actions inside the CRUD wrappers will fail!

### Utility Actions

You may want to put these actions in a library for reuse.

* NotificationListConcat - Concatenates a list of notifications to one string using StringBuilder.
* CRUDTemplatesCheck - Checks if a user is logged in and has the right role or an API Key is provided by an background process (timer or bpt)

## Adding a new entity and data actions to an application

### Preparation

1. If not already present, add the **CRUD Templates** application from the forge.
1. If not present copy the [Utility Actions](#utility-actions) to your application or library
1. If not present copy the **TimerKey** setting to your application or library
1. Determine the role that is authorized to perform the data actions and create it in **\<Your Application\>**
1. Add a **ValidationException** to **\<Your Application\>**
1. Add a **ConcurrentUpdateException** to **\<Your Application\>**
1. Copy **CRUDTemplatesCheck** and rename it to **\<yourrole\>Check**
1. Fix the error by checking the \<YourRole\>

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
1. Rename the structure to **\<new entity name\>CS** (Canonical Structure)

## UUID vs Autonumbers as Primary Key

Both UUIDs (Universally Unique Identifiers) and autonumbers (auto-incrementing integers) can be used as primary keys in a database, and each has its own set of advantages and disadvantages. The choice between them often depends on the specific requirements of the application and the characteristics of the data. Here are some pros and cons of using UUIDs and autonumbers as primary keys:

### UUIDs (Universally Unique Identifiers):

#### Pros:

1. **Uniqueness Across Systems:** UUIDs are designed to be globally unique, making them suitable for distributed systems. They can be generated independently on different machines without the risk of collision.
1. **Security:** UUIDs can be generated using secure algorithms, adding a level of security when the generation method is not easily predictable.
1. **No Centralized Authority:** UUIDs do not require a centralized authority for generation, which can be an advantage in decentralized or distributed systems.
1. **No Sequence Gaps:** Unlike autonumbers, UUIDs do not have gaps in the sequence, even if records are deleted. This can be beneficial in certain scenarios.

#### Cons:

1. **Storage Space:** UUIDs are typically larger than autonumbers (128 bits for UUIDs vs. 32 or 64 bits for integers), which can result in increased storage requirements, especially in large datasets.
1. **Human Readability:** UUIDs are not human-readable, which can make debugging and data exploration more challenging.
1. **Indexing Performance:** Indexing on UUIDs might not be as efficient as on integers, leading to slower query performance, especially in large datasets.

### Autonumbers (Auto-incrementing Integers):

#### Pros:

1. **Compact Storage:** Autonumbers are typically smaller in size compared to UUIDs, leading to more compact storage and potentially better performance in terms of storage space and indexing.
1. **Query Performance:** Integer-based keys often result in faster query performance, especially when used in joins or sorting operations.
1. **Human Readability:** Autonumbers are human-readable, which can be advantageous for developers during debugging and data exploration.

#### Cons:

1. **Limited Global Uniqueness:** Autonumbers are only unique within the scope of a single database, which can be a limitation in distributed systems.
1. **Potential Sequence Gaps:** Autonumbers may have gaps in the sequence if records are deleted, and this might impact certain business requirements or reporting.
1. **Centralized Authority:** Autonumbers typically rely on a centralized authority for generation, which can be a disadvantage in distributed or decentralized systems.

In conclusion, the choice between UUIDs and autonumbers as primary keys depends on the specific needs and constraints of your application. If global uniqueness and distribution are crucial, UUIDs might be a better choice. If compactness and query performance are more critical, autonumbers could be preferred. It's also not uncommon to use a combination, where a UUID is used for global uniqueness and autonumbers for local relationships or indexing.

[UUIDv7]: https://uuid7.com/

[Natural Key]: https://en.wikipedia.org/wiki/Natural_key
[How To Handle Concurrent Updates on Application Data Records]: https://success.outsystems.com/documentation/how_to_guides/data/how_to_handle_concurrent_updates_on_application_data_records/
[Why Auto Increment Is A Terrible Idea]: https://www.clever-cloud.com/blog/engineering/2015/05/20/why-auto-increment-is-a-terrible-idea/
[Primary Keys: IDs versus GUIDs]: https://blog.codinghorror.com/primary-keys-ids-versus-guids/
