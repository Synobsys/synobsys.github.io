---
layout: default
title: Common Glossary
sorting: 100
tags: [guide, glossary]
projectname: YourProjectName
---

# {{ page.title}}

## This glossary introduces {{page.projectname}} common terminology.

### [Aggregate](#aggregate)

1. A cluster of associated objects that are treated as a unit for the purpose of data changes. External references are restricted to one member of the AGGREGATE, designated as the root. A set of consistency rules applies within the AGGREGATE’S boundaries.

1. An OutSystems method to fetch data using an optimized query. Aggregates can load data from the server of the local database, and they support combining several Entities and advanced filtering. [Aggregate](https://success.outsystems.com/Documentation/11/Reference/OutSystems_Language/Data/Handling_Data/Queries/Aggregate)

---

### [Analysis Pattern](#analysis-pattern)

A group of concepts that represents a common construction in business modeling. It may be relevant to only one domain or may span many domains (Fowler 1997, p. 8).

---

### [Assertion](#assertion)

A statement of the correct state of a program at some point, independent of how it does it. Typically, an ASSERTION specifies the result of an operation or an invariant of a design element.

---

### [Design Pattern](#design-Pattern)

A description of communicating objects and classes that are customized to solve a general design problem in a particular context. (Gamma et al. 1995, p. 3)

---

### [Domain](#domain)

[Cambride Dictionary](https://dictionary.cambridge.org/dictionary/english/domain) definition:

An area of interest or an area over which a person has control:

* She treated the business as her private domain.
* These documents are in the public domain (= available to everybody).

[DDD Domain Driven Design](https://en.wikipedia.org/wiki/Domain-driven_design) defintion

A sphere of knowledge (ontology), influence, or activity. The subject area to which the user applies a program is the domain of the software.

---

### [Domain-Driven Design](#domain-driven-design)

An approach to software development that suggests that:

1. For most software projects, the primary focus should be on the domain and domain logic; and
1. Complex domain designs should be based on a [model](#model).

---

### [Domain Expert](#domain-expert)

A member of a software project whose field is the domain of the application, rather than software development. Not just any user of the software, the domain expert has deep knowledge of the subject.

---

### [Domain Layer](#domain-layer)

That portion of the design and implementation responsible for domain logic within a [layered architecture](#layered-architecture). The domain layer is where the software expression of the domain model lives.

---

### [Entity](#entity)

An object fundamentally defined not by its attributes, but by a thread of continuity and identity.

OutSystems [Entities](https://success.outsystems.com/Documentation/11/Developing_an_Application/Use_Data/Data_Modeling/Entities): Entities are elements that allow you to persist information in the database and to implement your database model. You can think of them as database tables or views.

An Entity is defined through Entity Attributes that store the information related to it. Examples of entity attributes are: Name, Address, Zip Code, City and so on.

---

### [Function](#function)

An operation that computes and returns a result without observable side effects.

---

### [Immutable](#immutable)

The property of never changing observable state after creation. implicit concept A concept that is necessary to understand the meaning of a model or design but is never mentioned.

---

### [Intention-Revealing Interface](#intention-revealing-interface)

A design in which the names of classes, methods, and other elements convey both the original developer’s purpose in creating them and their value to a client developer.

---

### [Iteration](#iteration)

A process in which a program is repeatedly improved in small steps. Also, one of those steps.

---

### [Layered Architecture](#layered-architecture)

A technique for separating the concerns of a software system, isolating a domain layer, among other things.

See the OutSystems [The Architecture Canvas](https://success.outsystems.com/Support/Enterprise_Customers/Maintenance_and_Operations/Designing_the_Architecture_of_Your_OutSystems_Applications/The_Architecture_Canvas)

---

### [Life Cycle](#life-cycle)

A sequence of states an object can take on between creation and deletion, typically with constraints to ensure integrity when changing from one state to another. May include migration of an [Entity](#entity) between systems.

---

### [Model](#model)

A system of abstractions that describes selected aspects of a domain and can be used to solve problems related to that domain.

---

### [Model-Driven Design](#model-driven-design)

A design in which some subset of software elements corresponds closely to elements of a model. Also, a process of codeveloping a model and an implementation that stay aligned with each other.

---

### [Modeling Paradigm](#modeling-paradigm)

A particular style of carving out concepts in a domain, combined with tools to create software analogs of those concepts (for example, object-oriented programming and logic programming).

---

### [Repository](#repository)

A mechanism for encapsulating storage, retrieval, and search behavior which emulates a collection of objects.

---

### [Responsibility](#responsibility)

An obligation to perform a task or know information (Wirfs-Brock et al. 2003, p. 3).

---

### [Service](#service)

An operation offered as an interface that stands alone in the model, with no encapsulated state.

---

### [Stateless](#Stateless)

The property of a design element that allows a client to use any of its operations without regard to the element’s history. A stateless element may use information that is accessible globally and may even change that global information (that is, it may have side effects) but holds no private state that affects its behavior.

---

### [Ubiquitous Language](#ubiquitous-language)

A language structured around the domain model and used by all team members to connect all the activities of the team with the software.

---

### [Value Object](#value-object)

An object that describes some characteristic or attribute but carries no concept of identity.

---
