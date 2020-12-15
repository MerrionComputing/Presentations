# Event Sourcing - around the edges

_Strategies for interactions between event sourced and single state model based systems_

## From event sourced systems to model based systems

### Projecting state

At its simplest the process of getting data from an event sourced system to a model based system is going to involve running a projection (or many projections) over the event sourced system and then writing the resultant state snapshot to the model based system as an "upsert".

A decision will need to be made about the frequency of this snapshotting and also how any merging with the existing model based data is done.  One strategy that can help is the idea of having a set of staging tables that the event sourced data is pushed into on each update allowing for a controlled merge thereafter.

### Turning events into commands



## From model based systems to event sourced systems

### Change feed subscription

Some model based systems (for example some relational databases) support a change feed - a way of sending out notifications whenever the underlying state model is changed.  _It is important to note that this change feed is conceptually different to event sourced data as it is focussed on what has changed rather than why)._

### Snapshots and deltas

Where a model based system does not support a change feed there will be a need to artificially create one yourself.  This involves keeping a local copy of whatever component(s) of that model based state you are interested in and periodically getting the current state of these components then comparing the two and, if differences exist, generating events accordingly.  The frequency of this operation will need to be decided on a business need basis but it should be granular enough to allow for a meaningful change history to be recreated.
