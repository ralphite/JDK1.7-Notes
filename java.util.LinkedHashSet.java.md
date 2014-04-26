##java.util.LinkedHashSet.java.md
----------

see the parent class HashSet which has most of the implementation.

To understand LinkedHashSet we need to understand LinkedHashMap.

The big difference from HashSet is LinkedHashSet guarantees a 
fixed order when iterating through the set.

Like HashSet, LinkedHashSet provides constant time performance for
the basic operations, including

- add
- contains
- remove

the performance is slightly less optimal comparing with HashSet
since LinkedHashSet has to maintain doubly linked lists running
through all of it's entries.

> one exception is iteration over the entire set. when doing so,
LinkedHashSet has better performance and time is proportional to
the size of the set, while for HashSet, the iteration time is 
proportional to the size of the set as well as the capacity of
the set (which is the capacity of the map used actually).

..

> also note this class is not synchronized. to synchronized, either
do it externally of use the Collections#synchronizedSet() method.

..

> Same as HashSet, the iterators returned by the iterator method
are **fail-fast**

