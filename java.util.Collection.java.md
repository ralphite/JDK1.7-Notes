##java.util.Collection.java.md
----------

- The root interface of the collection hierarchy.
- This interface is typically used to pass collections
around and manipulate them where maximum generality
is desired.

- There is no direct implementations of this interface.
However, `Bags` and `Multisets` (unordered collections
that may contain duplicate elements should implement
it directly.


methods (available in all collection types)

```
    int size();
    boolean isEmpty();
    boolean contains(Object o);
    Object[] toArray();
    <T> T[] toArray(T[] a);
    boolean add(E e);
    boolean remove(Object o);
    
    Iterator<E> iterator();
    
    boolean containsAll(Collection<?> c);
    boolean addAll(Collection<? extends E> c);
    boolean removeAll(Collection<?> c);
    boolean retainAll(Collection<?> c);
    void clear();
    
    boolean equals(Object o);
    int hashCode();
```

