##java.util.ListIterator.java.md
----------

This interface is an enhanced Iterator for lists with
the following features

- bi-directional traversing
- modifying the list during iteration
- obtain the iterator's current position

Methods specified

- boolean hasNext();
- E next();
- boolean hasPrevious();
- E previous();
- int nextIndex();
- int previousIndex();

> note the following remove method removes the element
returned by the last call of next or previous. This call
can only be made after the last call to next or previous.

- void remove();

> similar as remove, the set method also affects the last
element returned by next or previous, and it can be made 
only if neither remove nor add has been called after the
last call to next or previous.

- void set(E e);

> inserts the specified element at the implicit position,
which lies b/t returned values of nextIndex and previousIndex.
if the list is empty, the inserted value will become the
sole element.

- void add(E, e);
