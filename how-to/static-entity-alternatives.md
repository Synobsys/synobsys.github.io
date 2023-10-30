---
title: Static Entity Alternatives
---
# {{page.title}}

![decoration image](/how-to/images/image-from-rawpixel-id-50145-jpeg.jpg)

A computing best practice is not to use literals in your code. This is known as hard-coding and it makes it harder to maintain your code.

The default method to store a list of values in OutSystems is to use a Static Entity. The drawback of using static entities is that each static entity counts for an Application Object (AO). Since most licenses include a limited amount of AO's consider one of the alternatives to avoid using AO's for static entities.

This article describes the following alternatives:

1. [Constant local variables](#constant-local-variables)
1. [Constant functions](#constant-functions)
1. [JSON import](#json-import)
1. [Excel import](#excel-import)

## Constant local variables

For a single value you can just define a local variable and give it a default value. To emphasize its constant behavior you can prefix these local variables with **Constant**. E.g. **ConstantMaxRecords**

![Local var ConstantMaxRecords](/how-to/images/ConstantMaxRecords.png)

## Constant functions

When a literal is used multiple times you can create a Function Server Action that returns the fixed value. This may be useful for configuration values etc. Also here prefixing the name with **Constant** is used. E.g. **ConstantDefaultPageSize**.

Please note: When it's required to be able to change these values at runtime you should use site properties in O11 or Settings in ODC.

![Function Const_DefaultPageSize](/how-to/images/Function_ConstantDefaultPageSize.png)

## JSON import

When you require a record list you can import a JSON file and convert it to a structure list.

### Example Weekdays

We provide a JSON with the id and the name of the weekdays.

```json
[
  {"id": 1,"name": "Monday"},
  {"id": 2,"name": "Tuesday"},
  {"id": 3,"name": "Wednesday"},
  {"id": 4,"name": "Thursday"},
  {"id": 5,"name": "Friday"},
  {"id": 6,"name": "Saturday"},
  {"id": 7,"name": "Sunday"}
]
```

* In Service Studio we create a structure from json
![Add structure from json](/how-to/images/AddStructureFromJSon.png)
* Which gives us a weekday structure that we will use in our logic.
* Now import the json file in the resources folder.

Server Action **WeekDayGet**:

* In the logic tab we create a new folder "**Weekday**" in the server actions folder
* In this folder we create a new server action "**WeekdayGet**"" with output parameter "**Weekdays**"
* To improve performance set the property "Cache in minutes" a value e.g. 120

![Server Action Weekdays](/how-to/images/SA_Weekdays.png)

* Add a "**BinaryToText**" action to the logic, set parameter binary data to "**Resources.weekdays_json.Content**"
* Add a "**JSONDeserialize**" to convert the json to a weekday list
* Add a an "**assign**" to add the converted list to the output list

![WeekDayGet logic](/how-to/images/WeekDayGetLogic.png)

Server Action Function **WeekdayGetById**:

* Create a Server Action **WeekdayGetById** in the folder **Weekday**
* Add an input parameter **WeekdayId**, type integer
* Add an output parameter **Weekday**, type Weekday
* In the action flow add a server action **WeekdayGet**
* Add a **ListFilter** to filter the Weekday List on WeekDayId
* Raise an **Exception** if the day is not found
* **Assign** the found weekday from the list to the output parameter

![WeekdayGetById logic](/how-to/images/WeekDayGetById.png)

## Excel import

As an alternative we can import and convert an Excel file.

### Example Categories

Given an Excel file Categories with columns Name, Slug and Description we can create a Category structure and CategoryGet and CategoryGetBySlug functions.

* In the Data tab import the "**Categories.xlsx**" file
* Create a new structure "**Category**" with attributes:
    * **Name**
    * **Slug**
    * **Description**
* Create a server action **CategoryGet** with output parameter **Categories**
* Add an **ExcelToRecordList** action to the action flow
    * Record definition: **Category**
    * File content: **Resources.Categories_xlsx.Content**
* Assign the **ExcelToRecordList1** to **Categories**

![CategoryGet](/how-to/images/CategoryGet.png)

## Pros and Cons

Although the solutions above avoid consuming AO's it add extra complexity to your code. Extra logic is required for the following use cases:

* Joining in aggregates and sql queries
* Applying translations
* Multi-tenancy

In addition there can be a significant performance impact.

Therefore, make a careful consideration before choosing a static entity or one of the alternatives.

*[AO]: Application Object
*[O11]: OutSystems 11
*[ODC]: OutSystems Developer Cloud
