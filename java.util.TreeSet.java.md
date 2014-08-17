### java.util.TreeSet.java.md

`SortedSet`

- E first()
- E last()
- subSet(E from, E to)
- headSet(E to)
- tailSet(E from)

`NavigableSet`

- pollFirst()
- pollLast()
- ceiling(E e)
- floor(E e)

`TreeSet` is an implementation based on a TreeMap, like HashSet.

This implementation provides guaranteed log(n) time cost for the
basic operations.

One of the constructors can take a Comparator object for the 
comparision.
