---
title: User interface naming conventions
---

# {{page.title}}

## UI Flows

* no rules yet

## Screens

* Screen names start with the name of the (main) entity followed by a suffixes showing the purpose of the screen names. Use the following suffixes:
    * List - Listing instances e.g. `CustomerList`
    * Edit - for editing a record e.g. `CustomerEdit`
    * View - display a record e.g. `CustomerView`

* Set the name property of major elements such as:
    * Table
    * List
    * ShowRecords
    * EditRecords
    * TableRecords
    * Etc.
* Do not name every container!
* Action button text is specified on UX design and follows UX standards. In situations where no UX design is available, the following action button text applies:
    * **Save** to trigger the action to store the data of the current instance of an entity in the database
    * **Back** to cancel the action and return to the previous screen
    * **New** to start the creation of a new instance of an entity
    * **Delete** to either physical or logical remove the current instance from the database
    * **Edit** to start editing the current instance on an entity

## Blocks

* Reusable (web-)blocks have a name that describes their function followed by the suffix **Block** e.g **CustomerViewBlock**
