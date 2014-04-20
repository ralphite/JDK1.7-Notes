
- default non-arg constructor is surpressed to ensure non-instantiability
```
    private Arrays() {}
```
###Sorting
- primitive arrays can be sorted with dual-pivot quick sort which out performs normal single pivot quick sort in many situations. we can also specify fromIndex and toIndex
```
public static void sort(T[] a);
public static void sort(T[] a, int fromIndex, int toIndex);
//T can be byte, short, int, long, float, double and char
```

- Object types can be sorted with TimSort normally or a standard MergeSort if requested by user explicitly. We can also specify fromIndex and toIndex.
```
public static void sort(Object[] a);
public static void sort(Object[] a, int fromIndex, int toIndex);
public static <T> void sort(T[] a, Comparator<? super T> c);
public static <T> void sort(T[] a, int fromIndex, int toIndex, Comparator<? super T> c);
```
> **DuralPivotQuicksort** - a better quick sort
> **Timsort** - a better merge sort
> **LegacyMergeSort** - a standard merge sort which uses insertion sort when input size is less than 7

###Searching
