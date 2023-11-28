---
title: ADR 007 - Use UUID for primary keys
---
# {{page.title}}

* TOC
{:toc}

## Context

<!--
Describe here the forces that influence the design decision, including technological, cost-related, and project local.
-->

* [ ] TODO

## Decision

<!--
Describe here our response to these forces, that is, the design decision that was made. State the decision in full sentences, with active voice ("We will...").
-->
Use UUIDv7 as the primary key for all new tables (instead of sequential integer IDs).

* They can be freely exposed without disclosing sensitive information,
* they are not predictable
* and they are performant.

## Rationale

<!--Describe here the rationale for the design decision. Also indicate the rationale for significant *rejected* alternatives. This section may also indicate assumptions, constraints, requirements, and results of evaluations and experiments.
-->

* [ ] TODO

### Identity vs GUID

#### Identity

Pros:

* Small storage footprint
* Optimal join / index performance (e.g. for time range queries, most rows recently inserted will be on a limited number of pages)
* Highly useful for data warehousing
* Native data type of the OS, and easy to work with in all languages
* Easy to debug (`where userid = 457`)
* Generated automatically (retrieved through `SCOPE_IDENTITY()` rather than assigned)
* Not changeable.

Cons:

* Cannot be reliably "predicted" by applications — can only be retrieved after the INSERT
* Need a complex scheme in multi-server environments, since IDENTITY is not allowed in some forms of replication
* Can be duplicated, if not explicitly set to PRIMARY KEY
* If part of the clustered index on the table, this can create an insert hot-spot
* Proprietary and not directly portable
* Only unique within a single table
* Gaps can occur (e.g. with a rolled back transaction)

#### UUID

Pros:

* Unique across every table, every database, every server
* Allows easy merging of records from different databases
* Allows easy distribution of databases across multiple servers
* You can generate IDs anywhere, instead of having to roundtrip to the database
* Most replication scenarios require GUID columns anyway

Cons:

* It is a whopping 4 times larger than the traditional 4-byte index value; this can have serious performance and storage implications if you're not careful
* Cumbersome to debug `where userid='{BAE7DF4-DDF-3RG-5TY3E3RF456AS10}'`
* The generated GUIDs should be partially sequential for best performance (eg, `newsequentialid()` on SQL 2005) and to enable use of clustered indexes

### References

* [UUIDv7: The Time-Sortable Identifier for Modern Databases](https://uuid7.com/)
* [Why Auto Increment Is A Terrible Idea](https://www.clever-cloud.com/blog/engineering/2015/05/20/why-auto-increment-is-a-terrible-idea/)
* [Primary Keys: IDs versus GUIDs](https://blog.codinghorror.com/primary-keys-ids-versus-guids/)

## Status

* [x] **Proposed**
* [ ] Accepted
* [ ] Deprecated
* [ ] Superseded

<!--If deprecated, indicate why. If superseded, include a link to the new ADR.-->

## Consequences

<!--
Describe here the resulting context, after applying the decision. All consequences should be listed, not just the "positive" ones.
-->

* [ ] Must provide an O11 and ODC implementations
* [ ] Link to How to O11
* [ ] Link to how to ODC
