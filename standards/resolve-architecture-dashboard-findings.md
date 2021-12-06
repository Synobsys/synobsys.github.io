---
title: Resolve architecture dashboard findings
---

# Standard resolutions for architecture dashboard findings

Next follows a list with findings and agreed resolutions

Finding | Case | Resolution
---------|----------|---------
 Large Local Variable in ViewState | In BDD test | Resolve as wont fix reason For test purpose only.
 Unlimited records in Aggregate | Filter on unique index | Resolve as false positive reason: Filter on unique index.
 Unlimited records in Aggregate | Reference table with limited number of records e.g. 150 | Resolve as wont fix reason: Reference table alle records are required to facilitate select functionality.
