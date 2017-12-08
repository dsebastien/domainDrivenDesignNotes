# Terms

## Domain

The field for which a system is built.

## Domain model

A model for the domain.

## Domain-Driven Design \(DDD\)

Domain-driven Design \(DDD\) is a development approach that deeply values the domain model and connects it to the implementation

DDD was coined by Eric Evans

## Ubiquitous language

A set of terms used by all people involved in the domain, domain model, implementation and back-ends.

The idea is to avoid translation. As Eric Evans points out: "translation blunts communication and makes knowledge crunching anemic".

Every time we have to translate concepts between people, we lose a direct ability to think clearly about the thing we are building and to let new knowledge flow back and forth between domain and implementation.

Having a ubiquitous language makes communication clearer and allows teams to see more opportunities.

## Bounded context

A division of a larger system that has its own ubiquitous language and domain model.

Coined by Eric Erans. Bounded contexts provide a way to decompose a large, complex system into more manageable pieces. A large system is composed of multiple bounded contexts.

Each bounded context is the context for its own self-contained domain model, and has its own ubiquitous language.

A bounded context can also be seen as an autonomous business component defining clear consistency boundaries: one bounded context typically communicates with another bounded context by raising events.

## Context map

Context maps helps providing an overview of the whole system and helping people to understand the details of how different bounded contexts interact with each other.

## Entity

An entity or reference type is characterized by having an identity that's not tied to its attribute values. All attributes in an entity can change and it's still "the same" entity.

Two entities might be equivalent in all their attributes but still be distinct from each other.

## Value Object \(VO\)

A Value Object \(VO\) doesn't have a separate identity. A value object is only defined by its attribute values.

Native types are good examples of value objects. It is common to make VOs immutable.

From an event sourcing perspective, both entities and value objects play important roles in the domain, but only entities need to be persisted since only these may change.

## Aggregate

Some definitions:

* a larger unit of encapsulation than just a class
* a cluster of associated objects
  * example: model for a shopping cart: products, line items, quantity of a product
* a unit of a transaction boundary

Every transaction is scoped to a single aggregate

An aggregate handles commands, applies events and has a state model encapsulated within it that allow it to implement the required commands validation \(i.e., business rules\) of the aggregate.

Requiring a transaction to span across multiple aggregates doesn't make much sense, it usually means that the aggregates are not well defined:

* rethink aggregate boundaries
* review the responsibilities of each aggregate
* rethink the non-functional requirements of the system

A single command can't act on a set of aggregates.

An aggregate can't send events directly to other aggregates. Other aggregates might be interested by events of the other parts but should be listening on their own to avoid strong coupling.

Sharding can be made based on aggregates since they represent an isolated part of the system.

Aggregates have:

* input: you can communicate with them
* rules: invariants or business rules
* output: aggregate state
* behavior
* environment: context

## Aggregate Root

In DDD, an aggregate root is a consistent boundary around a set of system entities. They should be able to be loaded from persistence as a unit and saved as one.

Each aggregate forms a tree or graph of object relations. The aggregate root is the one at the top, which "speaks" for the whole and may delegate down to the rest. It's the one that the rest of the world communicates with.

An aggregate root is the entry point that accepts commands for an aggregate.

## Sagas \(aka Process Managers\)

* component that reacts to domain events in a cross-aggregate, eventually consistent manner \(time can also be a trigger\)
* sagas are sometimes purely reactive and sometime represent workflows
* a saga is a state machine driven forward by incoming events \(which may come from different aggregates\)
* some states will have side-effects \(e.g., sending commands, talking to external Web Services, sending e-mails, ...\)
* sagas are doing things that individual aggregates can't do
* coordinates the behavior of the aggregates in the domain
* subscribes to the events that the aggregates raise and then follow a set of rules to determine which command or commands to send
* do not contain any business logic, only logic necessary to choose which commands to send

## Transaction boundaries

Boundary within which you can assume that all the elements remain consistent with each other all the time.

To ensure the consistency of the system, transactions must succeed. To make sure of this, you need to ensure that the system is eventually consistent. Having reliable message delivery to aggregates is very important.

