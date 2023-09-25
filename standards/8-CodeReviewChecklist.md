---
title: OutSystem 11 Code review checklist
layout: default
---
# {{page.title}}

For use with ==OutSystem 11==

Use this checklist as an aid to the code review, but don't be limited to it. Give suggestions on how the code can be improved. Most important discuss the review result with your colleague and keep an open mind.

| Check | Rule |
| ---- | --- |
| 🔳 | No broken references shown in the [Broken References](https://www.outsystems.com/forge/component-overview/10062/broken-references) tool |
| 🔳 | No modules exists in application Independent Modules |
| 🔳 | Naming is in accordance with the [OutSystems Naming Conventions](OutSystemsNamingConventions.md) |
| 🔳 | All code and documentation is in English [ADR 2 standard language is English.](ADR-002-standard-language-is-English.md) |
| 🔳 | Have the best practices been applied. That is, it is built correctly and efficiently. |
| 🔳 | There are no hard coded values |
| 🔳 | There are Zero warnings. See the [Service Studio Warnings](https://www.outsystems.com/forge/component-overview/16101/service-studio-warnings) forge component to get a report of warnings for all modules |
| 🔳 | There is documentation explaining the decision to hide a warning. |
| 🔳 | No findings in Discovery |
| 🔳 | No findings in the [Architecture Dashboard](https://architecture.outsystems.com/) |
| 🔳 | [DevOps configuration](TBD) is updated. E.g. Turn Light BPT on, data export/import is described. |
| 🔳 | Unused dependencies are removed |

---

## Screen

| Check | Rule |
| ---- | --- |
| 🔳 | There is a clear description |
| 🔳 | Screen rendering is checked the browser zoom at 100% and all applicable screensizes for Tablets etc. (Chrome Developer Tools \<Ctrl + Shift + I\> and Toggle device toolbar \<Ctrl + Shift + M\> |
| 🔳 | The screen is compatible with the browsers defined in the project see or the OutSystems supported browsers [End User Requirements](https://success.outsystems.com/Documentation/11/Setting_Up_OutSystems/OutSystems_system_requirements#End_User_Requirements) for the OutSystems supported browsers |
| 🔳 | There is no inline CSS |
| 🔳 | All temporary CSS classes are replaced by Theme classes |
| 🔳 | There are no hard coded values in the screen actions |

---

## Actions

| Check | Rule |
| ---- | --- |
| 🔳 | There is a clear description |
| 🔳 | Is the name of the action self explanatory? |
| 🔳 |All variables have a clear description |
| 🔳 | Variable names are self explanatory |
| 🔳 | The action performs a single task |
| 🔳 | Does the action comply with the [Software that Fits in Your Head](https://youtu.be/4Y0tOi7QWqM) rules. |
| 🔳 | Are the action flow vertical and tidy. See [A code style guide for OutSystems](https://leonardo-monteiro-fernandes.medium.com/a-code-style-guide-for-outsystems-97a923084159) |
| 🔳 | Assigns and if statements have proper labels |
| 🔳 | Complex logic is clearly documented |
| 🔳 | Action flow is understandable without opening the elements |
| 🔳 | No upward flows are used if it's not a cycle |
| 🔳 | There are no hard coded values |
| 🔳 | Check if a cycle can be replaced by a list operation [“List” We Forget…](https://medium.com/productleague/list-we-forget-387fbd5173d4) |

---

## Queries (Aggregates and advanced SQL)

| Check | Rule |
| ---- | --- |
| 🔳 | The name is self explanatory |
| 🔳 | There is a clear description |
| 🔳 | Prefer aggregates only use SQL when the query is not possible with an aggregate or for bulk operations |
| 🔳 | Are filters as simple as possible? |
| 🔳 | Are the entities joined correct. Pay attention to the with or without clause. |
| 🔳 | Are the entities indexed properly |
| 🔳 | There are no hard coded values |
| 🔳 | Is the max records value set |

---

## Resources

| Check | Rule |
| ---- | --- |
| 🔳 | Have large resources such as Excel files and images been placed in a seperate module? |

---
