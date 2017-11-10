# Bounded Contexts

## Identification

Things to look for:

* natural boundaries in an organization: inside a bounded context, people collaborate and communicate closely; between bounded contexts the communication is less and often asynchronous
* same words being given different meanings

A bounded context should be strongly isolated from the rest of the system. Direct dependencies should be avoided.

Communication between bounded contexts should be done using commands/queries and events.



