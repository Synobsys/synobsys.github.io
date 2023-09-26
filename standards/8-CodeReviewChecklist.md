---
title: OutSystem 11 Code review checklist
layout: default
---
# {{page.title}}

For use with **OutSystem 11**

Use this checklist as an aid to the code review, but don't be limited to it. Give suggestions on how the code can be improved. Most important discuss the review result with your colleague and keep an open mind.

## Service Studio

* Are there no broken references shown in the [Broken References](https://www.outsystems.com/forge/component-overview/10062/broken-references) tool?
* Are there no modules in application Independent Modules?
* Is naming is in accordance with the [OutSystems Naming Conventions](OutSystemsNamingConventions.md)?
* Is all code and documentation is in [English](ADR-002-standard-language-is-English.md)?
* Have the best practices been applied. That is, it is built correctly and efficiently.
* Are there are no hard coded values?
* Are ther no warnings in Service Studio? See the [Service Studio Warnings](https://www.outsystems.com/forge/component-overview/16101/service-studio-warnings) forge component to get a report of warnings for all modules
* Is the decision to hide a warning documented?.
* Are there no findings in [Discovery](https://www.outsystems.com/forge/component-overview/409/discovery)?
* Are there no findings in the [AI Mentor Studio](https://architecture.outsystems.com/)?
* Is the [DevOps configuration](TBD) updated? E.g. Turn Light BPT on, data export/import is described.
* Have unused dependencies been removed?

---

## Screen

|   | Rule |
| - | ---- |
| <input type="checkbox"> | There is a clear description |
| <input type="checkbox"> | Screen rendering is checked the browser zoom at 100% and all applicable screensizes for Tablets etc. (Chrome Developer Tools \<Ctrl + Shift + I\> and Toggle device toolbar \<Ctrl + Shift + M\> |
| <input type="checkbox"> | The screen is compatible with the browsers defined in the project see or the OutSystems supported browsers [End User Requirements](https://success.outsystems.com/Documentation/11/Setting_Up_OutSystems/OutSystems_system_requirements#End_User_Requirements) for the OutSystems supported browsers |
| <input type="checkbox"> | There is no inline CSS |
| <input type="checkbox"> | All temporary CSS classes are replaced by Theme classes |
| <input type="checkbox"> | There are no hard coded values in the screen actions |

---

## Actions

|   | Rule |
| - | --- |
| <input type="checkbox"> | There is a clear description |
| <input type="checkbox"> | Is the name of the action self explanatory? |
| <input type="checkbox"> |All variables have a clear description |
| <input type="checkbox"> | Variable names are self explanatory |
| <input type="checkbox"> | The action performs a single task |
| <input type="checkbox"> | Does the action comply with the [Software that Fits in Your Head](https://youtu.be/4Y0tOi7QWqM) rules. |
| <input type="checkbox"> | Are the action flow vertical and tidy. See [A code style guide for OutSystems](https://leonardo-monteiro-fernandes.medium.com/a-code-style-guide-for-outsystems-97a923084159) |
| <input type="checkbox"> | Assigns and if statements have proper labels |
| <input type="checkbox"> | Complex logic is clearly documented |
| <input type="checkbox"> | Action flow is understandable without opening the elements |
| <input type="checkbox"> | No upward flows are used if it's not a cycle |
| <input type="checkbox"> | There are no hard coded values |
| <input type="checkbox"> | Check if a cycle can be replaced by a list operation [“List” We Forget…](https://medium.com/productleague/list-we-forget-387fbd5173d4) |

---

## Queries (Aggregates and advanced SQL)

|   | Rule |
| - | ---- |
| <input type="checkbox"> | The name is self explanatory |
| <input type="checkbox"> | There is a clear description |
| <input type="checkbox"> | Prefer aggregates only use SQL when the query is not possible with an aggregate or for bulk operations |
| <input type="checkbox"> | Are filters as simple as possible? |
| <input type="checkbox"> | Are the entities joined correct. Pay attention to the with or without clause. |
| <input type="checkbox"> | Are the entities indexed properly |
| <input type="checkbox"> | There are no hard coded values |
| <input type="checkbox"> | Is the max records value set |

---

## Resources

|   | Rule |
| - | ---- |
| <input type="checkbox"> | Have large resources such as Excel files and images been placed in a seperate module? |

---

    TODO Adapt en merge this list taken from <https://www.michaelegreiler.com>

## Implementation

* Does this code change do what it is supposed to do?
* Can this solution be simplified?
* Does this change add unwanted compile-time or run-time dependencies?
* Was a Forge component, API, library, service used that should not be used?
* Was a forge component, API, library, service not used that could improve the solution?
* Is the code at the right abstraction level?
* Is the code modular enough?
* Would you have solved the problem in a different way that is substantially better in terms of the code’s maintainability, readability, performance, security?
* Does similar functionality already exist in the codebase? If so, why isn’t this
functionality reused?
* Are there any best practices, design patterns or language-specific patterns
that could substantially improve this code?
* Does this code follow Object-Oriented Analysis and Design Principles, like the
[Single Responsibility Principle](https://en.wikipedia.org/wiki/Single-responsibility_principle), [Openclose Principle](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle), [Liskov Substitution Principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle), [Interface Segregation](https://en.wikipedia.org/wiki/Interface_segregation_principle), [Dependency Injection](https://en.wikipedia.org/wiki/Dependency_injection)? *How does this apply to OutSystems Code?*

## Dependencies

* If this change requires updates outside of the code, like updating the documentation, configuration, readme files, was this done?
* Might this change have any ramifications for other parts of the system, backward compatibility?

## Security and Data Privacy

* Does this code open the software for security vulnerabilities?
* Are authorization and authentication handled in the right way?
* Is sensitive data like user data, credit card information securely handled and stored?
* Is the right encryption used?
* Does this code change reveal some secret information like keys, passwords, or usernames?
* If code deals with user input, does it address security vulnerabilities such as cross-site scripting, SQL injection, does it do input sanitization and validation?Is data retrieved from external APIs or libraries checked accordingly?

## Logic Errors and Bugs

* Can you think of any use case in which the code does not behave as intended?
* Can you think of any inputs or external events that could break the code?

## Error Handling and Logging

* Is error handling done the correct way?
* Should any logging or debugging information be added or removed?
* Are error messages user-friendly?
* Are there enough log events and are they written in a way that allows for easy debugging?

## Testing and Testability

* Is the code testable?
* Does it have enough automated tests (unit/integration/system tests)?
* Do the existing tests reasonably cover the code change?
* Are there some test cases, input or edge cases that should be tested in
addition?

## Readability

* Was the code easy to understand?
* Which parts were confusing to you and why?
* Can the readability of the code be improved by smaller methods?
* Can the readability of the code be improved by different function/method or variable names?
* Is the code located in the right applicaton/module/folder?
* Do you think certain methods should be restructured to have a more intuitive control flow?
* Is the data flow understandable?
* Are there redundant comments?
* Could some comments convey the message better?
* Would more comments make the code more understandable?
* Could some comments be removed by making the code itself more readable?
* Is there any commented out code?
