# Command Handler Pipelines

A command can comprise a number of steps to be executed in sequence (or in parallel) with each step being able to succeed or fail.
Where a command step fails this may invoke a reversing action (also called a compensating action) to return the entity acted upon to the state it was in before the command was initiated.

Command handler pipelines do not act as transactions - that is to say changes made by a command pipeline are visible outside of that pipeline to any process querying the state of entities being operated upon by a command pipeline.

