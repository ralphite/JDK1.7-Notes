##java.util.Comparator.java.md
--------------

This interface serves as a comparison function which imposes
a **total ordering** on some collection of objects.

Comparators can be passed to sort methods such as
Collections#sort(List, Comparator) or
Arrays#sort(Object[], Comparator) for sorting purpose

Two methods are specified in this interface

- int compare(T a, T b);
- boolean equals(Object o);
