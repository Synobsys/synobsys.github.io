---
title: Architectural Decision Records
---
# {{page.title}}

<!--* TOC
{:toc}-->

An [Architectural Decision (AD)](https://en.wikipedia.org/wiki/Architectural_decision) is a software design choice that addresses a functional or non-functional requirement that is architecturally significant. An [Architecturally Significant Requirement (ASR)](https://en.wikipedia.org/wiki/Architecturally_significant_requirements) is a requirement that has a measurable effect on a software system’s architecture and quality. An **Architectural Decision Record (ADR)** captures a single AD, such as often done when writing personal notes or meeting minutes; the collection of ADRs created and maintained in a project constitute its decision log. All these are within the topic of Architectural Knowledge Management (AKM).

Note: The term “architecture decision record” can be used interchangeably.

See these articles for an explanation of Architecture Decision Records (ADR):

* <https://adr.github.io/>
* <https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions.html>

## Decision log (ADRs)

This document is used to track key decisions that are made during the course of the project. This can be used at a later stage to understand why decisions were made and by whom.

| Decision | Date | Alternatives considered | Reasoning | Detailed doc | Made by | Work Required |
| --- | --- | --- | --- | --- | --- | --- |
| A one-sentence summary of the decision made. | Date the decision was made. | A list of the other approaches considered. | A two to three sentence summary of why the decision was made. | A link to the ADR with the format [Title] DR. | Who made this decision? | A link to the work item for the linked ADR |
| Record architecture decisions | 2 Aug 2021 | - | | [ADR-001](ADR-001-documenting-architecture-decisions.md) | CoE | Log all decisions |
| Standard language is English | 2 Aug 2021 | Dutch language | Making English the standard language contributes to the maintainability of the applications | [ADR-002](ADR-002-standard-language-is-English.md) | CoE | - |
| Server Actions exposed to Reactive applications must be secured | 2 Aug 2021| Using a token | Public OutSystems Server Actions are exposed as REST services when consumed by Reactive or Mobile web applications. | [ADR-003](ADR-003-secure-core-services.md) | CoE | - |
| Use the BDD framework for Component testing | 2 aug 2021 | | There exist several Automated Testing Tools that are suitable for component testing. OutSystems recommends to use the BDD framework for Component testing and we accept this recommendation.| [ADR-004](ADR-004-bdd-framework-for-component-testing.md) | CoE | - |
| We will centralize all styling in the designated theme. | 2 aug 2021 | - | A Style Guide ensures a consistent look-and-feel across your applications, managing complexity, ensuring ease of use, and facilitating change. Only by centralizing the theme we can enforce the style guide. |  [ADR-005](ADR-005-centralized-styling.md) | CoE | Maintaining a centralized theme |
| We will only use forge components that are approved by the Center of Excellence | 2 aug 2021 | | | [ADR-006](ADR-006-approved-forge-components-only.md) | CoE | Get approval for using forge components that are not supported or trusted |
| Use UUIDv7 as the primary key for all new tables. | proposed | sequential integer IDs | todo | [ADR-007](ADR-007-uuid-primary-keys.md) | - | todo |
| We will use a common glossary to define the ubiquitous language as an essential part of the domain model. | proposed | - | todo | [ADR-008](ADR-008-common-glossary.md) | - | Maintain the glossary |
