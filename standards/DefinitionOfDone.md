---
title: Definition of Done
---

# {{page.title}}

* TOC
{:toc}

The Definition of Done (DoD) is used to determine when a task or user story is completed: DONE!

## When is a Task DONE?

* Coding is complete:
    * [ ] Coded in accordance with the [OutSystems development standards](index.md),
    * [ ] commented,
    * [ ] documented, (*TODO link to documentation guidelines*)
    * [ ] developer tested,
    * [ ] peer reviewed,
    * [ ] published without broken references and warnings

## When is a User story DONE?

* All tasks are completed;
* BDD tests written and passing. I.e. meeting the acceptance criteria.
* No (new) findings in [Discovery](https://www.outsystems.com/forge/component-overview/409/discovery)
* No technical debt added in [AI Mentor Studio](https://success.outsystems.com/documentation/11/managing_the_applications_lifecycle/manage_technical_debt/)
* No Service Studio Warnings
* **DevOps configuration** is updated. E.g. Turn Light BPT on, data export/import is described.

## When is a Sprint DONE?

* All User stories are done;
* Deployed to system test environment and passed system tests;
* Any build- deployment- configuration changes implemented documented and communicated.

You can use the [Code Review Checklist](8-CodeReviewChecklist.md) for your reviews.
