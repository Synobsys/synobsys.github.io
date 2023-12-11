---
title: ADR 8 - Common Glossary
---
# {{page.title}}

* TOC
{:toc}

## Context

<!--
Describe here the forces that influence the design decision, including technological, cost-related, and project local.
-->
Domain experts use their jargon while technical team members have their own language tuned for discussing the domain in terms of design.

The terminology of day-­‐to-­‐day discussions is disconnected from the terminology embedded in the code (ultimately the most important product of a software project). And even the same person uses different language in speech and in writing, so that the most incisive expressions of the domain often emerge in a transient form that is never captured in the code or even in writing.

Translation blunts communication and makes knowledge crunching anemic.

From [Domain-­‐Driven Design Reference](https://www.domainlanguage.com/product/domain-driven-design-reference/)

See <https://thedomaindrivendesign.io/developing-the-ubiquitous-language/>

## Decision

<!--
Describe here our response to these forces, that is, the design decision that was made. State the decision in full sentences, with active voice ("We will...").
-->
We will use a **common glossary** to define the ubiquitous language as an essential part of the domain model.

## Rationale

<!--Describe here the rationale for the design decision. Also indicate the rationale for significant *rejected* alternatives. This section may also indicate assumptions, constraints, requirements, and results of evaluations and experiments.
-->
When we all speak the same language in the project. There is less change of miscommunication or getting lost in translation.

See Martin Fowler's page on [Domain Driven Design](https://martinfowler.com/bliki/DomainDrivenDesign.html).

[![ddd book cover](/images/evans-book.jpg)](https://amzn.eu/d/aBpuCpU)

Also Eric Evans's 2003 book is an essential read for serious software developers

## Status

* [x] **Proposed**
* [ ] Accepted
* [ ] Deprecated
* [ ] Superseded

If deprecated, indicate why. If superseded, include a link to the new ADR.

## Consequences

<!--
Describe here the resulting context, after applying the decision. All consequences should be listed, not just the "positive" ones.
-->

We must keep a glossary of all terms and definitions in the bounded context the project thus creating an ubiquitous language.

We provided a [common glossary template](/common-glossary-template.md) to get you started.
