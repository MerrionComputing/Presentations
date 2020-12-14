# Event Sourcing - around the edges

_Strategies for interactions between event sourced and single state model based systems_

## From event sourced systems to model based systems

### Projecting state

At its simplest the process of getting data from an event sourced system to a model based system is going to involve running a projection (or many projections) over the event sourced system and then writing the resultant state snapshot to the model based system as an "upsert".

A decision will need to be made about the frequency of this snapshotting and also how any merging with the existing model based data is done.  One strategy that can help is the idea of having a set of staging tables that the event sourced data is pushed into on each update allowing for a controlled merge thereafter.

## From model based systems to event sourced systems

### Change feed subscription

### Snapshots and deltas
