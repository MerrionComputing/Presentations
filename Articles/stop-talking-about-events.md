# We need to STOP talking about events

*Event* sourcing, *event* driven architecture, domain *events*, integration *events*.... oh my.

## Event Sourcing

In an event sourced system the events are the source of the state(s) of the system.  This is fairly uncontroversial except that the events must, by definition, be past tense "things that have happened".  

If your business domain is one that understands the concept of ledgers then *Ledger Backed State* might be a better name.  If not, maybe use *History Derived State* ?
