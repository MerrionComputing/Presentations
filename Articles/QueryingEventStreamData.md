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

### Those that "Are currently x"

### Those that "Were ever x"

## "Who -> When -> What -> What" - the full query process
