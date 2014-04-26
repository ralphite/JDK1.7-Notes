##java.util.List.java.md
----------

Sub-interface of Collection. The following methods are added

- boolean addAll(int index, Collection<? extends E> c);
- E get(int index);
- E set(int index, E element);
- void add(int index, E element);
- E remove(int index);

> the following two methods for searching an element can be
O(n), thus are not very performant

- int indexOf(Object o);
- int lastIndexOf(Object o);

> ListIterator allows element insertion and replacement, and 
bidirectional access in addition to the normal operations that 
the Iterator interface provides. A method is provided to 
obtain a list iterator that starts at a specified position in 
the list.


- ListIterator<E> listIterator();
- ListIterator<E> listIterator(int index);



- List<E> subList(int fromIndex, int toIndex);
