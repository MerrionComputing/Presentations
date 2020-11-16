# How Event Sourcing makes for a better debugging experience for developers

## It started with a tweet....

![](../tweet-sourcing.jpg)

## Backstory: The airplane that crashed twice

## Event sourcing - making the hidden clues visible

Because event sourcing entails storing the history of all the actions that have occured to an entity and deriving the state from that it is possible to read back through that history in order to establish what the state was at a given point in time.  

## Making it even clearer

There are a couple of extra things you can do whenever you are working with event sourced systems which will make your debugging experience even better.  The first is to add correlation identifiers to any related events (for example events that come from the same command) which you can then use to search your event streams for all the matching events.

The second thing you can do is to include the "as-of" sequence number whenever you store the state of an entity or whenever you make a decision based on the state of an entity.  This allows you to look back over the event stream to get to the state _as it was_ at the time that the action was taken.
