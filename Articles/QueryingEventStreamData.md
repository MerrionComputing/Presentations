# Querying event stream data

## "What" - getting the state

In order to get an aspect of state from an event history you need to run a **projection** over that data.  

A projection is a piece of code that runs over the event stream for an entity in order to derive some state information about that entity.
For each event in the stream, in order, it needs to decide (a) am I interested in this kind of event and if so (b) what do I do with it.

For example a projection that was to get the **balance** of a bank account would be interested in **deposit** and **withdrawal** events for (a) and would increase or decrease the current balance by the amount of the deposit or withdrawal for (b).


## "When" - getting the state as at a point in time

The event stream of an entity is immutable in that the only change that can be performed is to append new events onto the end of it.  This means that any projection which has been run up to a given point in that event stream will give the same result if run again at a future date.

This also allows you to query the state of an entity _as at a given point in time_ just as easily as querying the state for the current moment in time.  It is good practice always to return the _as at x_ information whenever you run a projection.

## "Who" - deciding which entities to include in the query

In an SQL query the data returned are conceptually filtered by the WHERE part of the query after they are returned.  (The reality is far more complicated than this, but the conceptual model is basically that).
In an event sourced system you need to decide which projections you are qoing to run over which event streams before getting the data.

### All

A special case is where you want to run a projection over all the event streams.  Most event sourcing systems will give you some way of retrieving all the event streams as built in functionality.

### Known fixed set

Where your query is to be run for a pre-known fixed set of event streams you can simply supply them as input parameters to the query of have a configuration file containing that set.

### Those that "Are currently x"

A more common type fo query constraing is to perform a query "for those event streams that are in a given state x".  Doing this type of query requires a two-step process where we run a projection to get the value of "are in a given state x" and then pass on those to the next step in the query. 

### Those that "Were ever x"

Using the immutability of event streams we can also perform a query "for those event streams that were every in a given state x".  This is an incredibly powerful aspect of querying over event streams and something that would be really difficult to do in an SQL present-tense state system.

## "Who -> When -> What -> What Next" - the full query process

The full process of querying an event stream based system then becomes a series of steps with the final step being "what do you do with the projections you ran".  It might be as simple as returning a row for each one or you can apply some form of aggregation functionality (SUM, AVG etc.) as required.

## Comparing queries

By storing the query instance itself on an event stream and storing the data returned from each step as events in that event stream it is possible to repeat a query at a later date and to then compare the two query event streams to find what components of the result itself have changed between runs.  In financial services systems this is a very powerful capability.
