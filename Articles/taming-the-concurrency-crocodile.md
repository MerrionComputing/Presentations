# Taming the Concurrency Crocodile

## What is the **problem**?

At its most basic a computer program can be broken down into two components: first get the current state and then perform some action based on that state.  The problem with this is that this takes a finite amount of time which means there is a risk that the current state you are acting on may not be current any more.

It isn't really a defect as such but more an innevitable fact that we have to be aware of and take steps to mitigate.  I have called it a concurrency crocodile as a crocodile is an ambush predator that catches the unwary.

## Solution 1: **Transactions**

The traditional solution to the concurrency crocodile is to perform the get-then-set steps inside of a database transaction so that we are guaranteed to be working on the latest state.  In a transaction, _as viewed from the outside_, the whole thing either happens or does not happen.

Within a transaction you want to do as little work as you can, as they do become a performance bottle neck in a large or distributed system.  You also need to plan for what you are going to do if the transaction gets rolled back for any reason - if a _real world_ thing has happened and you have no record of it this may be as serious as a concurrency error.

## Solution 2: **Locks on crocs**

An alternative that is very closely related to transactions is to use writer locks to ensure that only one process is allowed to write to an event stream at any given point in time.  This guarantees that if you have acquired the lock then no other party can come along and change your state whilst you were processing based on it.

This solution does require some way of "unlocking" the event stream if an erroroccurs which leaves it in a locked state - this can be a manual process or a lock trimming process.

However both transactions and locks solve the concurrency problem by **change prevention** – which is not always something that your particular business can tolerate.  An alternative approach is to detect when a concurrency issue has occured and to repair the event stream so as to fix it.


## Solution 3: **Undo**, redo, undo etc.

## Solution 3b: **Re-run** on fault

## Solution 4: Look **behind** you

## Wrapping it up

## Other possibilities

