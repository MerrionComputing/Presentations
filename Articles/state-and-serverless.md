# State and Serverless

Very broadly speaking, every serverless function falls into one of four categories:  

## Pure serverless

The output of the function depends solely on some action(s) performed over the input(s) to the function.  These range from something simple such as a function to add numbers together to something more complicated such as a data encryption function.  These functions have no need for any stored state at all and the inputs are private to the process so not subject to any mutation whilst the function (or function chain) is executing.

## State change commands

These functions take some input values and alter some persisted state.  This persisted state can be private or shared in a database, a file etc.  In an **event sourced** application this command will append one or more events to the event streams of whatever state is being changed.

## Decision based state change commands

These functions get the current state of some entity (or entities), make a decision based on that state and then update some state accordingly.  An example of this might be a command to apply interest to a bank balance based on the balance held at the time that the command is executed.  As discussed in [Taming the Concurrency Crocodile](taming-the-concurrency-crocodile.md) this type of serverless command needs to be coded to allow for the possibility that teh state being acted upon might have changed whilst the command was running.

## Decision based commands with side effects

These functions act on an existing state and/or input parameters to trigger an action to take place external to the function.  For exampel a function to delete a file or to send an email might fall into this catregory.  Although these functions don't have to save local state it is considered good practice for them to store an audit trail of any actions they trigger so that there is a reduced chance of duplicate actions.

## Persisted state

Where a serverless function needs access to persisted state there are two ways that this can be achieved - either by a _shared present state_ such as a file or database record, or by a _shared event history_ as used in **event sourced** state systems.

For an event sourced state that is being used in a serverless system my recomendation would be only to create the state (by running a projection) when it is going to be used - in effect an entity only needs to have a state when that state is being queried or used.
