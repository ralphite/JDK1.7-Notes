##java.util.ArrayList.java.md
----------------

ArrayLists permit null. This class is roughly equivalent to Vector
except that it's **not synchronized**.

O(1) time methods:

- size and isEmpty
- get and set
- iterator and listIterator

add(E) is of *amortized* O(1) time complexity.

All others are roughly O(n), including

- trimToSize()
- ensureCapacity(int)
- contains(Object), indexOf(Obj) and lastIndexOf(Obj)
- clone()
- toArray(...)
- add(int, Object)
- remove(int) and remove(Object)
- clear(), removeAll(..), addAll(..), retainAll(..)

The constant factor of ArrayList is lower than the one of LinkedList.

The ArrayList instance has to be **synchronized externally** in concurrent
context, or wrapped with `Collections.synchronizedList` at creation
time:

```
List list = Collections.synchronizedList(new ArrayList(...));
```

Similar to other collection types, the Iterators and ListIterators
returned from iterator() and listIterator() are **fail-fast**.

Internally, ArrayList uses an Object array to store data and the
default capacity is only 10.

>note line 115 and 152 where a static final constant is used to
save memory

ArrayList can accept any collection as parameter when constructing
a new instance.

>>note line 236 that capacity is increased to 1.5 times each time
the array is full

```
int newCapacity = oldCapacity + (oldCapacity >> 1);
```

>>note that capacity is an int and the max value is Integer.MAX_VALUE - 8.

..

>>>>!!!use the clone() method to create a copy of an ArrayList

..

>>note line 483 to set array elements to null so that GC can reclaim
the memory

..

>>note the usage of System.arraycopy for fast array copying
