# Taming the Concurrency Crocodile

## What is the **problem**?

At its most basic a computer program can be broken down into two components: first get the current state and then perform some action based on that state.  The problem with this is that this takes a finite amount of time which means there is a risk that the current state you are acting on may not be current any more.

It isn't really a defect as such but more an innevitable fact that we have to be aware of and take steps to mitigate.  I have called it a concurrency crocodile as a crocodile is an abush predator that catches the unwary.

## Solution 1: **Transactions**

The traditional solution to the concurrency crocodile is to perform the get-then-set steps inside of a database transaction so that we are guaranteed to be working on the latest state.  

## Solution 2: **Locks on crocs**

## Solution 3: **Undo**, redo, undo etc.

## Solution 3b: **Re-run** on fault

## Solution 4: Look **behind** you

## Wrapping it up

## Other possibilities

