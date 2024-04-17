---
title: Standard resolutions for AI Mentor Studio findings
---

# {{page.title}}

Architecture Dashboard is now renamed to AI Mentor Studio

See this article how to [Properly Dispositioning OutSystems Architecture Dashboard Findings]

Next follows a list with findings and agreed resolutions:

| Finding | Case | Resolution | Reason in AI Mentor Studio |
| --- | --- | --- | --- |
| Large Local Variable in ViewState | In BDD test | Resolve as wont fix | For test purpose only. |
| Unlimited records in Aggregate | Filter on unique index | Resolve as false positive | Filter on unique index. |
| Unlimited records in Aggregate | Reference table with limited number of records e.g. 150 | Resolve as wont fix | Reference table all records are required to facilitate select functionality. |

[Properly Dispositioning OutSystems Architecture Dashboard Findings]: https://medium.com/@jmjames/properly-dispositioning-outsystems-architecture-dashboard-findings-e3b7db1aca34
