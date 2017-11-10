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

## Entity

An entity or reference type is characterized by having an identity that's not tied to its attribute values. All attributes in an entity can change and it's still "the same" entity.

Two entities might be equivalent in all their attributes but still be distinct from each other.

## Value Object \(VO\)

A Value Object \(VO\) doesn't have a separate identity. A value object is only defined by its attribute values.

Native types are good examples of value objects. It is common to make VOs immutable.

From an event sourcing perspective, both entities and value objects play important roles in the domain, but only entities need to be persisted since only these may change.

## Aggregate

A larger unit of encapsulation than just a class.

Every transaction is scoped to a single aggregate

An aggregate handles commands, applies events and has a state model encapsulated within it that allow it to implement the required commands validation \(i.e., business rules\) of the aggregate.

Requiring a transaction to span across multiple aggregates doesn't make much sense, it usually means that the aggregates are not well defined:

* rethink aggregate boundaries
* review the responsibilities of each aggregate
* rethink the non-functional requirements of the system

A single command can't act on a set of aggregates.

An aggregate can't send events directly to other aggregates. Other aggregates might be interested by events of the other parts but should be listening on their own to avoid strong coupling.

Sharding can be made based on aggregates since they represent an isolated part of the system.

## Aggregate Root

The aggregate forms a tree or graph of object relations.

The aggregate root is the one at the top, which "speaks" for the whole and may delegate down to the rest. It's the one that the rest of the world communicates with.



