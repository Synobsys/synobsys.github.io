---
title: how to create entity bdd tests from a stencil
---

# How to create entity bdd tests from a stencil

Use this how to to create bdd tests for an entity's database actions

Decide if you require a new test block module or want to extend an existing one.

## Create a tests in a new core widgets modules

1. To create a new module open module `Stencil_Entity_Tests_CW` in ServiceStudio
1. Click Module Clone
1. Close module `Stencil_Entity_Tests_CW`
1. Rename the module to <domain>_<concept>_<entitygroup>_tests_cw e.g. `RA_SampleConceptDemoMasterTests_CW`
1. Publish the module
1. In ServiceStudio open application Independent Modules
1. Move the new application to your test application e.g. `RA Sample Concept Tests`
1. Open the Manage Dependencies (Ctrl+Q)
1. Add a dependency to the entity to test its dababase actions
1. Switch to the data tab (Ctrl+4)
1. Locate the `Stencil_CoreServices_Pat/TemplateEntity` and find usages (F12)
1. Replace all usages with <YourEntity>
1. Ignore all errors for now
1. For each `Stencil_CoreServices_Pat\TemplateEntityDbActions\<dbServerAction>` replace with the corresponding `<YourConcept_CS\<yourEntity>DbActions\<dbServerAction>`
1. Remove the unused dependencies from `Stencil_CoreServices_Pat`
1. Use (Ctrl+R) to replace `TemplateEntity` with '<yourEntity>`
1. Open and fix all errors. E.g. replace FunctionalKey with your functional key attribute.
1. Open Manage Dependencies (Ctrl+Q)
1. Add a dependency to \<YourDomain\>_DomainSecurity_FS \<YourEntityEditRole\>
1. Go to the logic tab (Ctrl+3) and locate the `TemplateRole`
1. Find all `TemplateRole` usages (F12)
1. Relplace all with `YourEntityEditRole`
1. Publish your module
1. Open your TestSuite module e.g. `RA_SampleConcept_Tests`
1. Manage dependencies (Ctrl+Q)
1. Add a dependency to <YourEntity>Scenarios
1. Open the TestSuite screen
1. In the widget tree add a new container and name it <YourEntity>Tests
1. Insert a text widget and set the text to : "Feature As a <concept>administrator I can maintain <yourentity"
1. Insert the scenario web blocks
1. Publish the module
1. Open the TestSuite screen in your browser and check that all tests have completed with success.

## Create tests in an existing module

### Core Service test steps

1. Open your concept core test module e.g. `RA_CoreConcept_Tests_CS`
1. Open module (Ctrl+O) `Stencil_Entity_Tests_CW`
1. Switch to the logic tab (Ctrl+3)
1. Open the logic tab (Ctrl+3)
1. Copy the folder `TemplateEntityBDDDataActions`
1. Switch to your cs module and paste the folder into the ServerAction folder
1. Open the logic tab (Ctrl+3)
1. Paste into the Server Actions folder
1. Open the manage dependencies window (Ctrl_Q)
1. Add a dependency to
    1. `<YourEntity>`_CreateOrUpdate
    1. `<YourEntity>`_Delete
    1. `<YourEntity>`_Remove
1. Expand the Stencil_CoreServices_Pat Server Actions
1. Expand folder TemplateEntityDBActions
1. Find (F12) and replace the following actions:
    1. TemplateEntity_CreateOrUpdate with `<YourEntity>`_CreateOrUpdate
    1. TemplateEntity_Delete with `<YourEntity>`_Delete
    1. TemplateEntity_Remove with `<YourEntity>`_Remove
1. Select the Stencil_CoreServices_Pat actions folder,  right mouse click -> Remove unused dependencies
1. Switch to the data tab (Ctrl+4)
1. Locate the Stencil_CoreServices_Pat \ TemplateEntity
1. Find all usages (F12)
1. Replace all usages with <YourEntity>
1. Select the Stencil_CoreServices_Pat Database folder,  right mouse click -> Remove unused dependencies
1. Check that there are no more dependencies to module Stencil_CoreServices_Pat
1. Find and Replace (Ctrl+R) `TemplateEntity` with `YourEntity`
1. Fix all errors by replacing the nonexisting "FunctionalKey" with `YourEntity` functional key attribute
1. Do all todo's and remove them when done.
1. Publish the module (F5)
1. Close the module

### Test widget steps

1. Open your test core widgets module e.g. `RA_SampleConceptTests_CW`
1. Open the manage dependencies window (Ctrl+q)
1. Add a dependency to all the `<yourentity>` BDDDataActions
1. Go back to module `Stencil_Entity_Tests_CW`
1. Switch to the data tab (Ctrl+4)
1. Make sure the folder `TemplateEntityTestData` is collapsed
1. Copy the folder `TemplateEntityTestData`
1. Switch to your module's data tab (Ctrl+4) and paste the folder in the Database folder.
1. Go back to module `Stencil_Entity_Tests_CW`
1. Switch to the Interface tab (Ctrl+2)
1. Copy UIFlow `TemplateEntity_Scenarios`
1. Manage Dependencies (Ctrl_q)
1. Add dependencies to `YourEntity`DBActions
1. Find all usages (F12) for the TemplateEntityDBActions and replace them with `YourEntity`DBActions
1. Switch to the logic tab (Ctrl+3) and locate the folder `TemplateEntityBDDDataActions`
1. Replace all the ServerActions with the corresponding action from your core concept test cs module e.g. `RA_CoreConcept_Tests_CS`
1. Switch to the data tab (Ctrl_4)
1. Locate the TemplateEntityTestData folder and replace all static entities with your copy of the static entities
1. Locate TemplateEntity and find all usage (F12
1. Replace all usages with `YourEntity`
1. Remove the `Stencil_Entity_Tests_CW` unused dependencies
1. Replace (Ctrl+R) "TemplateEntity" with `<yourentityname>`
1. Fix all errors
    1. Can't identify 'FunctionalKey' element in expression.: Replace with your entities functional key attribute e.g. Code
    1. A valid expression must be set for parameter 'DemoMasterFunctionalKey'. => Use Unused argument ...
1. Publish (F5) your module

1. Switch to the Interface tab (Ctrl+2)
1. Make sure all ui flows are collapsed
1. Select both the `TemplateEntityScenarios` UIFlow
1. Copy the UIFlow
1. Go to your CW module and switch to the Interface (Ctrl+2)
1. Paste the UIFlows in the UI Flows folder
1. Ignore all errors
1. Close Module `Stencil_Entity_Tests_CW`
1. Open the Manage Dependencies (Ctrl+Q)
1. Add a dependency to the entity to test its database actions
1. For each `Stencil_CoreServices_Pat\TemplateEntityDbActions\<dbServerAction>` replace with the corresponding `<YourConcept_CS\<yourEntity>DbActions\<dbServerAction>`
1. Switch to the data tab (Ctrl+4)
1. Locate the `Stencil_CoreServices_Pat/TemplateEntity` and find usages (F12)
1. Replace all usages with <YourEntity>
1. Ignore all errors for now
1. Remove the unused dependencies from `Stencil_CoreServices_Pat`
1. Use (Ctrl+R) to replace `TemplateEntity` with '<yourEntity>`
1. Open and fix all errors. E.g. replace FunctionalKey with your functional key attribute.
1. Open Manage Dependencies (Ctrl+Q)
1. Add a dependency to \<YourDomain\>_DomainSecurity_FS \<YourEntityEditRole\>
1. Go to the logic tab (Ctrl+3) and locate the `TemplateRole`
1. Find all `TemplateRole` usages (F12)
1. Relplace all with `YourEntityEditRole`
1. Publish your module
1. Open your TestSuite module e.g. `RA_SampleConcept_Tests`
1. Manage dependencies (Ctrl+Q)
1. Add a dependency to <YourEntity>Scenarios
1. Open the TestSuite screen
1. In the widget tree add a new container and name it <YourEntity>Tests
1. Insert a text widget and set the text to : "Feature As a <concept>adminstrator I can maintain <yourentity"
1. Insert the scenario web blocks
1. Publish the module
1. Open the TestSuite screen in your browser and check that all tests are succesfull.
