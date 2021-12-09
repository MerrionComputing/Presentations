# We need to STOP talking about events

*Event* sourcing, *event* driven architecture, domain *events*, integration *events*.... oh my.

## Event Sourcing

In an event sourced system the events are the source of the state(s) of the system.  This is fairly uncontroversial except that the events must, by definition, be past tense "things that have happened".  They must also be kept for as long as they are needed to recreate a state.  

If your business domain is one that understands the concept of ledgers then *Ledger Backed State* might be a better name.  If not, maybe use *History Derived State* ?

## Event Driven Architecutre

In an event driven architecture, events are emitted by one part of a system and other part(s) act on receipt of those events.  In this usage an event is present tense and there is no expectation that it should be kept forever.  

## Domain Events

## Integration Events

Integration events are sent between domains, or between (micro)services to keep them in synch with each other's internal state - which we need to do because every domain or (micro)service must own its own private copy of whatever state it relies upon.  Sometimes these are used to trigger an action in the recipient as well in which case they become more like a *command*.

