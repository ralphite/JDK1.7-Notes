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
- fill an array with a specific value, can also provide fromIndex and toIndex

```
public static void fill(Object[] a, Object val);
public static void fill(Object[] a, int fromIndex, int toIndex, Object val);
```

###Cloning
- has many `copyOf` and `copyOfRange` methods which use the `System.arraycopy` native method

```
public static int[] copyOf(int[] original, int newLength);
public static <T> T[] copyOfRange(T[] original, int from, int to);
public static <T,U> T[] copyOfRange(U[] original, int from, int to, Class<? extends T[]> newType);
```

```
public static native void arraycopy(Object src,  int  srcPos, 
            Object dest, int destPos, int length);
//this method copies an array very fast and truncates or pads 
//with 0s or nulls when necessary to ensure output length
```

> `System.arraycopy` uses assemblies which can operate on multiple elements with one asm directive.
> see http://hg.openjdk.java.net/jdk7u/jdk7u/hotspot/file/98fafba890cb/src/share/vm/prims/jvm.cpp#l309
> and https://gutspot.com/2011/11/16/system-arraycopy%E6%BA%90%E7%A0%81%E5%88%86%E6%9E%90/

###Convert to List
- a private static class ArrayList which extends List is defined

```
List l = Arrays.asList(new LinkedList(), new ArrayList(), new Object(), 1, 2, 4);
```

###hashCode, deepHashCode and deepEquals
- `hashCode`'s return value is based on the hashCode of all the hashCode of the elements, e.g.

```
    public static int hashCode(Object a[]) {
        if (a == null)
            return 0;

        int result = 1;

        for (Object element : a)
            result = 31 * result + (element == null ? 0 : element.hashCode());

        return result;
    }
```

> ***31*** is the most frequently used prime factor to calc hashCode

- `deepHashCode` recursively calc the hashCode if it's an array of arrays. it doesn't work if an array constains itself.
- `deepEquals` is similar to `deepHashCode` which works well with nested arrays of arbitrary depth

###toString and deepToString
- the `toString` methods are not recursive and concatenates the toString value of all the elements
- the `deepToString` method works well with nested arrays of arbitrary depth. The implementation can detect recursive definitions, that is, an array which contains itself directly or indirectly, and prints `[...]` in this case, thus it is safe.

> the implementation is quite interesting. it uses a HashSet to contain all the current arrays being processed. When it begins the array object is put into the set, and after it finishes the array object is removed.


> how to create an array which contains itself? `Object[] o = new Object[1]; o[0] = o;` is an example.
