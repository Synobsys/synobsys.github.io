---
title: How-to get started with BDD test framework
---

# How-to get started with BDD test framework

**IMPORTANT!**

* Before you start watch this <a class="external" href="https://www.outsystems.com/events/tech-talks/designing-application-testing/" target="_blank">How to Design Tests in OutSystems</a> in depth tech talk.
* You **must read** the [BDD framework documentation](https://www.outsystems.com/forge/Component_Documentation.aspx?ProjectId=1201&ProjectName=bddframework) and **do the exercises** in your personal environment.

## Setup the BDD framework

1. Install the [BDD framework](https://www.outsystems.com/forge/component-overview/1201/bddframework) from the Forge
1. Install the BDD framework reporting tool TBD forge component
    * To install the BDD framework reporting tool go to <yourdevserver>/servicecenter/Applications_List.aspx and click on the publish application button. Upload the "BDD Framework Reporting.oap" and 1-Click Publish

    ![Publish BDD Framework Application](images\PublishBDDFrameworkApplication.png)

1. Set the BDD framework rest api effective url

    * In Service Center open the BDDFrameworkReporting module and open the integrations tab
    * Navigate to the Consumed REST APIs section and open the BDDFrameworkV1 REST API
    * Set the effective url to your environment base url e.g., `https://synobsys.outsystemscloud.com/`

1. Set the Timer_ExecuteNewRoundOfTestSuites schedule and activate the timer

    * In Service Center open the BDDFrameworkReporting module and open the timers tab
    * Click on the Timer_ExecuteNewRoundOfTestSuites
    * Enter the desired schedule e.g. daily at 01:00 h
    * Click on Activate to activate the timer if it is not active

## Writing test scenarios

Refer to the OutSystems [Top-Notch Acceptance Criteria](https://success.outsystems.com/Documentation/11/Managing_the_Applications_Lifecycle/Test_Automation_in_the_Delivery_Lifecycle#Top-Notch_Acceptance_Criteria) section for guidance on writing acceptance criteria.
We create test scenarios based on the acceptance criteria written in the [Given When Then](https://www.agilealliance.org/glossary/gwt) format.

## Creating a new test suite

### Create Test Suite application

In LifeTime create a new application using the bddframework template.

* Open your LifeTime environment Applications screen: `<yourlifetimeserver>`/lifetime/Applications.aspx
* Click on the button Create Application ![Create Application screenshot](images\CreateApplicationInLifeTime.png)
* Create a new application parameters:
    * Choose owner team: The team you application to test belongs to e.g., Talent Manager Team
    * Choose the environment: Development
    * What are you building? : BDDFramework
    * Give the app a name following the [naming convention](..\standards\OutSystemsNamingConventions.html)
    * Fill the description.
    * Upload an icon. (We recommend to use the same icon as the application with a test watermark added)

* Open the new application in ServiceStudio and create a new BDDFramework module name it like the module you are testing with the suffix `_Test`
* In the MainTestFlow add a new screen and select the BDDFramework Data Drive Scenario (Static Enitity) template and name it `TestSuite`. Please note that you ***must*** name the screen `TestSuite` for the reporting tool to work.

![Create TestSuite Screen](images\CreateTestSuiteScreen.png)

* This action also adds a WebBlock `DataDrivenDb_Scenario` that we keep as a template
Together with this webblock a static entity named TestData is created and an aggregate is added to the preparation.

* Open the `TestSuite` screen and remove the `ScenarioListRecords` from the widget tree
* Move the WebBlock to the templates UIFlow
* Delete the GetTestData aggregate from the preparation
* Set the module description to "`<tested module name>` tests module using BDDFramework"
* Publish the module

### Create Core Test Services

In LifeTime create a new application using the service template.

* Open your LifeTime environment Applications screen: `<yourlifetimeserver>`/lifetime/Applications.aspx
* Click on the button Create Application ![Team Create App screenshot](images\CreateApplicationInLifeTime.png)
* Create a new application parameters:
    * Choose owner team: The team you application to test belongs to
    * Choose the environment: Development
    * What are you building? : Choose a service template e.g, Service, CoreServices_CS
    * Name: `<tested module name>` Core Tests
    * Description: Wrapper of common reused tests logic
    * Upload an icon. (We recommend to use the same icon as the application with a test watermark added)

TODO Adjust howto from here!

* Publish the Module

## Building a test scenario example

**Feature:** As a Talent Manager I should be able to manage skill and categories

**Scenario:** Add Skill Group

**Given** I am a Talent Manager

**When** I add a new Skill Group  named "Play"

**Then** I should be able to get a successful result

### Preparation steps

#### Create reusable actions in module TalentManagerCoreTests_CS

* `UserTalentManagerGetOrCreate`: Gets or creates (if not already existing) a Talent Manager user. _Please note that as an exception we will **not** remove the user in the Teardown of the tests as this may interfere with other running tests and will polute the users administration._
* `SkillGroupSampleGet`: Initializes a sample Skill Group record with given fields

### Implement the scenario

* Copy the Sample_Test webblock and rename it to `TalentManagerAddSkillGroup`
* Set the names of the Scenario and the Given-When-Then blocks: ![Scenario Add SkillGroup image](images\ScenarioAddSkillGroup.png)
* Add the following logic to the a_Setup screen action: ![Setup action flow screenshot](images\SetupScreenAction.png)
* Add the following logic to the b_Given screen action:
    * Add an Assert webblock to the flow and set the name to AssertTalentManager
    * Set Expected to: `"User is TalentManager"`
    * Set Obtained to: `"User is " +
If(LoggedInUserId = NullIdentifier(), "not logged in",
If(CheckTalentManagerRole(LoggedInUserId), "", "not a ")) + "TalentManager"`

* Add the following logic to the c_When screen action: ![When action flow screenshot](images\WhenScreenAction.png)
* Add the following logic to the d_Then screen action:
    * Add an Assert webblock to the flow and set the name to `AssertSkillGroupCreated`
    * Set Expected to `"SkillGroup record created successfully"`
    * Set Obtained to `"SkillGroup record " +
If(CreatedSkillGroupId <> NullIdentifier(), "created successfully", "not created")`
* Add the following logic to the e_Teardown screen action: ![Teardown action flow screenshot]()
    * Call SkillGroupDelete if a record was created

## Adding test suites to the BDD framework reporting tool

To add a test suite to the BDD framework reporting tool you must add the module names separated with a comma to the ModuleListCSV site property. E.g. `TalentManager_CS_Tests`

<!--
# Example

_As a Store Manager I should be able to manage my
products and categories_

**Scenario:** Search shop products

**Given** that my shop has multiple wine products **and** one of those is an Altos de Luzon (Red)

**When** I search for the keywords "altos de"

**Then** I should get 1 single result containing Altos de Luzon (Red)

_As a Store Manager I should be able to manage my products and
categories_

**Scenario Outline:** Search shop products

**Given** that my shop has multiple wine products

**When** I search for the keywords “<Keywords>”

**Then** I should get <Number of Results>

Examples:

| Keywords | Number of Results |
| -------- | -- |
| Altos de | 1 |
| Altos | 3 |
| Hormigas | 2 |
-->

## Reference

* <a href="https://www.agilealliance.org/glossary/gwt" target="_blank">Given When Then</a>
* <a href="https://success.outsystems.com/Documentation/11/Managing_the_Applications_Lifecycle/Test_Automation_in_the_Delivery_Lifecycle" target="_blank">Test Automation in the Delivery Lifecycle</a>
* <a href="https://success.outsystems.com/Documentation/Best_Practices/OutSystems_Testing_Guidelines/Component_Testing" target="_blank">Component Testing</a>
