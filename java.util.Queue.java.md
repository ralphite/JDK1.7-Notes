##java.util.Queue.java.md
--------

methods specified

- add/offer
- remove/poll
- element/peek

three basic functions, each with two methods.
the first one throws an exception if fails,
the 2nd one returns specific values instead
(false, null)

in most implementations, there is no size limit
to the queues, in which case the two sets of
methods are the same.

in some capacity-restricted implementations,
the latter set `offer`/`poll`/`peek` is better
since we don't need to handle the exceptions
