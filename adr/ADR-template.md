---
title: ADR N - brief decision title
---
# {{page.title}}

**Date**: dd/mm/yyyy
<!-- The date the decision was made.
-->

## Status

[x] **Proposed**
[ ] Accepted
[ ] Deprecated
[ ] Superseded
If deprecated, indicate why. If superseded, include a link to the new ADR.
<!--
A proposed design can be reviewed by the development team prior to accepting it. A previous decision can be superseded by a new one, or the ADR record marked as deprecated in case it is not valid anymore.
-->

## Context

<!--
Describe here the forces that influence the design decision, including technological, cost-related, and project local.

The text should provide the reader an understanding of the problem, or as Michael Nygard puts it, a value-neutral [an objective] description of the forces at play.

Example:

Due to the microservices design of the platform, we need to ensure consistency of logging throughout each service so tracking of usage, performance, errors etc. can be performed end-to-end. A single logging/monitoring framework should be used where possible to achieve this, whilst allowing the flexibility for integration/export into other tools at a later stage. The developers should be equipped with a simple interface to log messages and metrics.

If the development team had a data-driven approach to back the decision, i.e. a study that evaluates the potential choices against a set of objective criteria by following the guidance in Trade Studies, the study should be referred to in this section.
-->

## Decision

<!--
Describe here our response to these forces, that is, the design decision that was made. State the decision in full sentences, with active voice ("We will...").

The decision made, it should begin with 'We will...' or 'We have agreed to ....

Example:

We have agreed to utilize Serilog as the Dotnet Logging framework of choice at the application level, with integration into Log Analytics and Application Insights for analysis.
-->

## Rationale

<!--Describe here the rationale for the design decision. Also indicate the rationale for significant *rejected* alternatives. This section may also indicate assumptions, constraints, requirements, and results of evaluations and experiments.
-->

## Consequences

<!--
Describe here the resulting context, after applying the decision. All consequences should be listed, not just the "positive" ones.
-->
