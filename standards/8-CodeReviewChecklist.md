---
title: OutSystem 11 Code review checklist
layout: default
---
# {{page.title}}

For use with **OutSystem 11**

Use this checklist as an aid to the code review, but don't be limited to it. Give suggestions on how the code can be improved. Most important discuss the review result with your colleague and keep an open mind.

### Solar System Exploration, 1950s – 1960s

- [ ] Mercury
- [x] Venus
- [x] Earth (Orbit/Moon)
- [x] Mars
- [ ] Jupiter
- [ ] Saturn
- [ ] Uranus
- [ ] Neptune
- [ ] Comet Haley

|   | Rule |
| --- | ---- |
| - [ ] | No broken references shown in the [Broken References](https://www.outsystems.com/forge/component-overview/10062/broken-references) tool |
| <input type="checkbox"> | No modules exists in application Independent Modules |
| <input type="checkbox"> | Naming is in accordance with the [OutSystems Naming Conventions](OutSystemsNamingConventions.md) |
| <input type="checkbox"> | All code and documentation is in English [ADR 2 standard language is English.](ADR-002-standard-language-is-English.md) |
| <input type="checkbox"> | Have the best practices been applied. That is, it is built correctly and efficiently. |
| <input type="checkbox"> | There are no hard coded values |
| <input type="checkbox"> | There are Zero warnings. See the [Service Studio Warnings](https://www.outsystems.com/forge/component-overview/16101/service-studio-warnings) forge component to get a report of warnings for all modules |
| <input type="checkbox"> | There is documentation explaining the decision to hide a warning. |
| <input type="checkbox"> | No findings in Discovery |
| <input type="checkbox"> | No findings in the [AI Mentor Studio](https://architecture.outsystems.com/) |
| <input type="checkbox"> | [DevOps configuration](TBD) is updated. E.g. Turn Light BPT on, data export/import is described. |
| <input type="checkbox"> | Unused dependencies are removed |

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
