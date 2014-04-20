
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

> the array must be sorted already. the return value is the index of key if found, otherwise, `-(insertion_piont) - 1`

- like sorting, elements in primitive arrays can be searched with standard binary search
```
public static int binarySearch(PrimitiveType[] a, PrimitiveType key);
public static int binarySearch(PrimitiveType[] a, int fromIndex, int toIndex, PrimitiveType key);
```

- same for Object arrays
```
public static int binarySearch(Object[] a, Object key);
public static int binarySearch(Object[] a, int fromIndex, int toIndex, Object key);
```

- we can also provide an explicit `Comparator`
```
public static <T> int binarySearch(T[] a, T key, Comparator<? super T> c);
public static <T> int binarySearch(T[] a, int fromIndex, int toIndex, T key, Comparator<? super T> c);
```

> `>>>` is used to divide 2
>```
>int mid = (low + high) >>> 1;
>```

###Equality Testing
- array objects' `equals` method is inherited from Object which simply compares the object location. We can use the static equals methods defined in this class for a *better* equality testing
```
public static boolean equals(PrimitiveTypes[] a, PrimitiveTypes[] a2);
//PrimitiveTypes can be byte, short, int, long, char, boolean, double and float
public static boolean equals(Object[] a, Object[] a2);
```

> How two doubles or floats are compared
>```
>if (Double.doubleToLongBits(a[i])!=Double.doubleToLongBits(a2[i]))
>                return false;
> //and
>if (Float.floatToIntBits(a[i])!=Float.floatToIntBits(a2[i]))
>                return false;
>```

###Filling


###Cloning


###Convert to List


###hashCode, deepHashCode and deepEquals


###toString and deepToString
