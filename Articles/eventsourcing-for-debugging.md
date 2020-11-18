# How Event Sourcing makes for a better debugging experience for developers

## It started with a tweet....

I wrote this tweet last weekend after I had been doing some investigating of a sporadic defect in a piece of software I have been working on for a few years: 

![](../tweet-sourcing.jpg)

It got quite a reaction so I thought I would expand on it to explain the how and the why of this statement.

## Time, the great disruptor

Once you have passed the stage of educated guesswork the next process in diagnostic debugging of a production issue involves attempting to recreate the state as at which the defect manifested itself and then stepping through the code from that state so as to _catch the bug in the act_ as it happened.  This is both difficult and time consuming.

## Event sourcing - making the hidden clues visible

Because event sourcing entails storing the history of all the actions that have occured to an entity and deriving the state from that it is possible to read back through that history in order to establish what the state was at a given point in time.  This really comes into its own when you are debugging a situation where one process changes an entity state and a subsequent process changes it back again.  

## Making it even clearer

There are a couple of extra things you can do whenever you are working with event sourced systems which will make your debugging experience even better.  The first is to add correlation identifiers to any related events (for example events that come from the same command) which you can then use to search your event streams for all the matching events.

The second thing you can do is to include the "as-of" sequence number whenever you store the state of an entity or whenever you make a decision based on the state of an entity.  This allows you to look back over the event stream to get to the state _as it was_ at the time that the action was taken.
