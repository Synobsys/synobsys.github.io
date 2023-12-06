---
title: OutSystem 11 Code review checklist
layout: default
---
# {{page.title}}

For use with **OutSystem 11**

Use this checklist as an aid to the code review, but don't be limited to it. Give suggestions on how the code can be improved. Most important discuss the review result with your colleague and keep an open mind.

***TODO Adapt en merge this list taken from <https://www.michaelagreiler.com/>***

* TOC
{:toc}

## Implementation

* [ ] Does this code change do what it is supposed to do?
* [ ] Can this solution be simplified?
* [ ] Does this change add unwanted compile-time or run-time dependencies?
* [ ] Was a Forge component, API, library, service used that should not be used?
* [ ] Was a forge component, API, library, service not used that could improve the solution?
* [ ] Is the code at the right abstraction level?
* [ ] Is the code modular enough?
* [ ] Would you have solved the problem in a different way that is substantially better in terms of the code’s maintainability, readability, performance, security?
* [ ] Does similar functionality already exist in the codebase? If so, why isn’t this
functionality reused?
* [ ] Are there any best practices, design patterns or language-specific patterns
that could substantially improve this code?

## Dependencies

* [ ] Were updates to documentation, configuration, or readme files made as required by this change?
* [ ] Are there any potential impacts on other parts of the system or backward compatibility?

## Security and Data Privacy

* [ ] Does this code open the software for security vulnerabilities?
* [ ] Are authorization and authentication handled in the right way?
* [ ] Is sensitive data like user data, credit card information securely handled and stored?
* [ ] Is the right encryption used?
* [ ] Does this code change reveal some secret information like keys, passwords, or usernames?
* [ ] If code deals with user input, does it address security vulnerabilities such as cross-site scripting, SQL injection, does it do input sanitization and validation?Is data retrieved from external APIs or libraries checked accordingly?

## Logic Errors and Bugs

* [ ] Can you think of any use case in which the code does not behave as intended?
* [ ] Can you think of any inputs or external events that could break the code?

## Error Handling and Logging

* [ ] Is error handling done the correct way?
* [ ] Should any logging or debugging information be added or removed?
* [ ] Are error messages user-friendly?
* [ ] Are there enough log events and are they written in a way that allows for easy debugging?

## Ethics and Morality

* [ ] Does this change make use of user data in a way that might raise privacy concerns?
* [ ] Does the change exploit behavioral patterns or human weaknesses?
* [ ] Might the code, or what it enables, lead to mental and physical harm for (some) users?
* [ ] If the code adds or alters ways in which people interact with each other, are appropriate measures in place to prevent/limit/report harassment or abuse?
* [ ] Does this change lead to an exclusion of a certain group of people or users?
* [ ] Does this code change introduce any algorithm, AI, or machine learning bias?
* [ ] Does this code change introduce any gender/racial/political/religious/ableist bias?

## Testing and Testability

* [ ] Is the code testable?
* [ ] Have automated tests been added, or have related ones been updated to cover the change in functionality?
* [ ] Do the existing tests reasonably cover the code change (unit/integration/system tests)?
* [ ] Are there some test cases, input, or edge cases that should be tested in addition?

## Readability

* [ ] Was the code easy to understand?
* [ ] Which parts were confusing to you and why?
* [ ] Can the readability of the code be improved by smaller methods?
* [ ] Can the readability of the code be improved by different function/method or variable names?
* [ ] Is the code located in the right applicaton/module/folder?
* [ ] Do you think certain methods should be restructured to have a more intuitive control flow?
* [ ] Is the data flow understandable?
* [ ] Are there redundant comments?
* [ ] Could some comments convey the message better?
* [ ] Would more comments make the code more understandable?
* [ ] Could some comments be removed by making the code itself more readable?
* [ ] Is there any commented out code?

## Usability and Accessibility

* [ ] Is the proposed solution well designed from a usability perspective?
* [ ] Is the API well documented?
* [ ] Is the proposed solution (UI) accessible?
* [ ] Is the API/UI intuitive to use?

## Performance

* [ ] Do you think this code change will impact system performance in a negative way?
* [ ] Do you see any potential to improve the performance of the code?

## Experts Opinion

* [ ] Do you think a specific expert, like a security expert or a usability expert, should look over the code before it can be committed?
* [ ] Will this code change impact different teams? Should they have a say on the change as well?

## Module

* [ ] Are there no broken references shown in the [Broken References](https://www.outsystems.com/forge/component-overview/10062/broken-references) tool?
* [ ] Is the module placed in the right application? Excluding Independent Modules?
* [ ] Is naming is in accordance with the [OutSystems Naming Conventions](OutSystemsNamingConventions.md)?
* [ ] Is all code and documentation is in [English](ADR-002-standard-language-is-English.md)?
* [ ] Have the best practices been applied. That is, it is built correctly and efficiently.
* [ ] Are there are no hard coded values?
* [ ] Are ther no warnings in Service Studio? See the [Service Studio Warnings](https://www.outsystems.com/forge/component-overview/16101/service-studio-warnings) forge component to get a report of warnings for all modules
* [ ] Is the decision to hide a warning documented?.
* [ ] Are there no findings in [Discovery](https://www.outsystems.com/forge/component-overview/409/discovery)?
* [ ] Are there no findings in the [AI Mentor Studio](https://architecture.outsystems.com/)?
* [ ] Is the [DevOps configuration](TBD) updated? E.g. Turn Light BPT on, data export/import is described.
* [ ] Have unused dependencies been removed?

---

## Screen

* [ ] Is there is a clear description?
*Is the screen rendering checked in the browser zoom at 100% and all applicable screensizes for Tablets etc. (Chrome Developer Tools \<Ctrl + Shift + I\> and Toggle device toolbar \<Ctrl + Shift + M\>?
* [ ] Is the screen compatible with the browsers defined in the project or the OutSystems supported browsers? See [End User Requirements](https://success.outsystems.com/Documentation/11/Setting_Up_OutSystems/OutSystems_system_requirements#End_User_Requirements) for the OutSystems supported browsers |
* [ ] Is there no inline CSS?
* [ ] Are all temporary CSS classes replaced by Theme classes?
* [ ] Are there no hard coded values in the screen actions?

---

## Actions

* [ ] Is there is a clear description for the action?
* [ ] Is the name of the action self explanatory?
* [ ] Do all variables have a clear description?
* [ ] Are the variable names are self explanatory?
* [ ] Does the action perform a single task?
* [ ] Does the action comply with the [Software that Fits in Your Head](https://youtu.be/4Y0tOi7QWqM) rule.?
* [ ] Is the action flow vertical and tidy. See [A code style guide for OutSystems](https://leonardo-monteiro-fernandes.medium.com/a-code-style-guide-for-outsystems-97a923084159)?
* [ ] Do assigns and if statements have proper labels?
* [ ] Is complex logic clearly documented?
* [ ] Is the action flow understandable without opening the elements?
* [ ] Are there no upward flows except when used if it's a cycle?
* [ ] Are ther no hard coded values?
* [ ] Is there a cycle that can be replaced by a list operation [“List” We Forget…](https://medium.com/productleague/list-we-forget-387fbd5173d4)?

---

## Queries (Aggregates and advanced SQL)

* [ ] Is the name is self explanatory?
* [ ] Is there a clear description?
* [ ] Is advanced sql used that could be replaced with an aggregate? Prefer aggregates only use SQL when the query is not possible with an aggregate or for bulk operations.
* [ ] Are filters as simple as possible?
* [ ] Are the entities joined correct? Pay attention to the with or without clause.
* [ ] Are the entities indexed properly?
* [ ] Are there are no hard coded values?
* [ ] Is the max records value correctly set?

---

## Resources

* [ ] Have large resources such as Excel files and images been placed in a seperate module?
